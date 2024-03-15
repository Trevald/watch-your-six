<template>
    <AppDisplay :mode="mode" :value="value" />
    <AppSettings :settings="settings" @change="updateSettings" />
</template>

<script>
import AppDisplay from "./components/AppDisplay.vue";
import AppSettings from "./components/AppSettings.vue";

export default {
    components: { AppDisplay, AppSettings },

    data() {
        return {
            mode: "number", // number|color
            intervall: 3, // in ms
            currentNumber: undefined,
            currentColor: undefined,
            minNumber: 1,
            maxNumber: 9,
        };
    },

    computed: {
        settings() {
            return {
                mode: this.mode,
                intervall: this.intervall,
                minNumber: this.minNumber,
                maxNumber: this.maxNumber,
            };
        },

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
            setTimeout(this.setNumber, this.intervall * 1000);
        },

        start() {
            this.setNumber();
        },

        setNumber() {
            const newNumber = this.getRandomNumber();
            if (newNumber === this.currentNumber) {
                this.setNumber();
                return;
            }
            this.currentNumber = newNumber;

            this.setTimer();
        },

        updateSettings(data) {
            console.log(data);
            this.intervall = data.intervall;
            this.minNumber = data.minNumber;
            this.maxNumber = data.maxNumber;
        },
    },

    mounted() {
        this.start();
    },
};
</script>
