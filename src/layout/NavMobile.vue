<script setup>
import ButtonMain from './../components/ButtonMain.vue';
</script>

<template>
    <div class="hamburger-menu">
        <button class="hamburger-button">
            <span></span>
        </button>
        <nav>
            <ul>
                <li>Features</li>
                <li>Pricing</li>
                <li>Resources</li>
            </ul>
            <ul>
                <li><ButtonMain :hasBG = false>Login</ButtonMain></li>
                <li><ButtonMain>Sign Up</ButtonMain></li>
            </ul>
        </nav>
    </div>
</template>

<style scoped lang="scss">
    li {
        list-style: none;
    }
</style>