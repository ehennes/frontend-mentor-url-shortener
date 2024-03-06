<script setup>
    defineProps({
        hasBG: {
            type: Boolean,
            default: true
        },
        btnAlt: {
            type: Boolean,
            default: false
        }
    });
</script>

<template>
    <button :class="[hasBG && 'add-bg', btnAlt && 'btn-alt']">
        <slot></slot>
    </button>
</template>

<style scoped lang="scss">
    button {
        background: none;
        border: none;
        color: var(--violet-gray);
        cursor: pointer;
        font-size: 15px;
        font-weight: 900;
        transition: all ease 0.3s;

        &:hover {
            color: var(--dark-violet);
        }

        &.add-bg {
            background: var(--cyan);
            border-radius: 25px;
            color: #fff;
            padding: 8px 20px;

            &:hover {
                background: var(--cyan-hover);
            }
        }

        &.btn-alt {
            border-radius: 5px;
        }
    }
</style>