<template>
    <AppDisplay :mode="mode" :value="value" />
</template>

<script>
import AppDisplay from "./components/AppDisplay.vue";

export default {
    components: { AppDisplay },

    data() {
        return {
            mode: "number", // number|color
            intervall: 3000, // in ms
            currentNumber: undefined,
            currentColor: undefined,
            minNumber: 1,
            maxNumber: 99,
        };
    },

    computed: {
        value() {
            switch (this.mode) {
                case "number":
                    return this.currentNumber;
                    break;
                case "color":
                    return this.currentColor;
                    break;
                default:
                    return undefined;
                    break;
            }
        },
    },

    methods: {
        getRandomNumber() {
            const min = this.minNumber;
            const max = this.maxNumber;
            return Math.floor(Math.random() * (max - min + 1) + min);
        },

        setTimer() {
            setTimeout(this.setNumber, this.intervall);
        },

        start() {
            this.setNumber();
        },

        setNumber() {
            this.currentNumber = this.getRandomNumber();
            this.setTimer();
        },
    },

    mounted() {
        this.start();
    },
};
</script>
