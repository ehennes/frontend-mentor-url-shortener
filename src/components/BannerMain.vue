<script setup>
    import ButtonMain from './ButtonMain.vue';
</script>

<template>
    <section class="banner">
        <h2>
            <slot></slot>
        </h2>
        <ButtonMain>
            Get Started
        </ButtonMain>
    </section>
</template>

<style scoped lang="scss">
    .banner {
        align-items: center;
        display: flex;
        flex-direction: column;
        padding: 50px 0;
        position: relative;

        &:before {
            background-color: var(--violet);
            background-image: url('./../../public/images/bg-boost-desktop.svg');
            background-position: 50% 50%;
            background-repeat: no-repeat;
            background-size: cover;
            content: '';
            height: inherit;
            inset: 0;
            left: 50%;
            position: absolute;
            transform: translate3d(-50%, 0, 0);
            width: 100vw;
            z-index: -1;
        }
    }

    h2 {
        color: #fff;
        margin-bottom: 25px;
        text-align: center;
    }
</style>