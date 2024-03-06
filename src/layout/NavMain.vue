<script setup>
    import ButtonMain from './../components/ButtonMain.vue';
</script>

<template>
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
</template>

<style scoped lang="scss">
    nav {
        display: flex;
        flex-basis: 90%;
        justify-content: space-between;
    }

    ul {
        align-items: center;
        display: flex;
        gap: 30px;
    }

    li {
        font-size: 15px;
        font-weight: 700;
        list-style: none;
        transition: all ease 0.3s;

        &:hover {
            color: var(--dark-violet);
        }
    }
</style>