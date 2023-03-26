<script setup>
    import { ref } from 'vue';

    import { Block } from '../Block';
    import { StopButton } from '../StopButton';
    import { StartButton } from '../StartButton';
    import { PauseButton } from '../PauseButton';
    import { Text } from '../Text';

    const value = ref(0);
    const status = ref('idle');

    let intervalId = 0;

    const onStart = () => {
        if (!['idle', 'paused'].includes(status.value)) {
            return;
        }

        status.value = 'started';

        intervalId = setInterval(() => {
            value.value++;
        }, 1000)
    }

    const onStop = () => {
        if (!['started', 'paused'].includes(status.value)) {
            return;
        }

        clearInterval(intervalId);
        status.value = 'idle';
        value.value = 0;
    }

    const onPaused = () => {
        if (status.value !== 'started') {
            return;
        }

        clearInterval(intervalId);
        status.value = 'paused';
    }

    const formatValue = value => {
        const milli = value * 1000;

        const hours = Math.floor(milli / 3600000);
        const minutes = Math.floor((milli % 3600000) / 60000);
        const seconds = minutes > 0 ? (milli - (minutes * 60000)) / 1000 : value;

        return `${hours > 0 ? `${hours}:` : ''}${minutes > 0 ? `${minutes}:` : ''}${seconds}`;
    };
</script>

<template>
    <Block>
        <div class="Timer">
            <Text :is-active="status === 'started'">{{ formatValue(value) }}</Text>
            <div :class="{ Timer_Separator: true, Timer_Separator__active: status === 'started' }"></div>
            <div class="Timer_Buttons">
                <StartButton :onClick="onStart" v-if="status !== 'started'" />
                <PauseButton :onClick="onPaused" v-if="status === 'started'" />
                <StopButton :onClick="onStop" :is-active="status === 'started'" />
            </div>
        </div>
    </Block>
</template>

<style scoped>
    .Timer{
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: space-between;
        column-gap: 50px;
        height: 100%;
        width: 100%;
    }

    .Timer_Separator {
        height: 0px;
        border: 1px solid #9E9E9E;
        width: 100%;
    }

    .Timer_Separator__active {
        border: 1px solid #ffffff;
    }

    .Timer_Buttons {
        display: flex;
        align-items: center;
        justify-content: center;
        column-gap: 50px;
    }
</style>
