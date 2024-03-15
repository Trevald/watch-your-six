<template>
    <div class="display">
        <span class="value">{{ value }}</span>
    </div>
</template>

<script>
export default {
    props: ["mode", "value"],
};
</script>

<style scoped>
.display {
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;

    display: flex;
    justify-content: center;
    align-items: center;

    background-color: #242429;
}

.value {
    font-size: min(90vh, 90vw);
    line-height: 1.25em;
    color: #ffee44;
    text-align: center;
}
</style>
