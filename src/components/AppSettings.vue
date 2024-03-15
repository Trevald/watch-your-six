<template>
    <button @click="toggle" type="button" class="button-settings">
        Settings
    </button>
    <div class="app-settings" v-if="active">
        <div class="content">
            <div class="form-group">
                <label for="input-intervall"
                    >Intervall ({{ intervall }}s)</label
                >
                <input
                    type="range"
                    min="1"
                    max="10"
                    step="1"
                    v-model="intervall"
                    @input="handleChange"
                />
            </div>
        </div>

        <div class="actions">
            <button @click="toggle" type="button">Done</button>
        </div>
    </div>
</template>

<script>
export default {
    props: ["settings"],
    emits: ["change"],

    data() {
        return {
            mode: this.settings.mode,
            intervall: this.settings.intervall,
            minNumber: this.settings.minNumber,
            maxNumber: this.settings.maxNumber,
            active: false,
        };
    },

    methods: {
        handleChange($e) {
            this.$emit("change", {
                mode: this.mode,
                intervall: this.intervall,
                minNumber: this.minNumber,
                maxNumber: this.maxNumber,
            });
        },

        toggle() {
            this.active = !this.active;
        },
    },
};
</script>

<style scoped>
.app-settings {
    position: fixed;
    z-index: 10;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;

    display: flex;
    flex-direction: column;
    justify-content: center;

    color: rgba(255, 255, 255, 0.8);
    background-color: #242429;
}

.content {
    padding: 2vw;
    flex: 0 0 auto;
}

.actions {
    padding: 4vw 2vw;
    display: flex;
    flex: 0 0 auto;
    justify-content: center;
}

.form-group {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 2vw;
}

label {
    font-size: 3vw;
    font-weight: normal;
    text-align: center;
}

input[type="range"] {
    width: 80%;
}

button {
    appearance: none;
    border: none;
    box-shadow: none;
    border-radius: 100vw;
    background-color: rgb(0, 100, 255);
    font-weight: bold;
    color: white;
    padding: 2vw 4vw;
    min-width: 20vw;
    font-size: 2vw;
}

.button-settings {
    position: fixed;
    z-index: 5;
    bottom: 1rem;
    right: 1rem;

    font-size: 1rem;
    padding: 1rem;
    min-width: unset;

    color: rgba(255, 255, 255, 0.4);
    background-color: rgba(255, 255, 255, 0.1);
}
</style>
