<script setup>
import ButtonMain from './../components/ButtonMain.vue';

const openMenu = () => {
    document.querySelector('.hamburger-button').classList.toggle('menu-open');
}

</script>

<template>
    <div class="hamburger-menu">
        <button @click="openMenu" class="hamburger-button">
            <span class="top-bar"></span>
            <span class="middle-bar"></span>
            <span class="bottom-bar"></span>
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
    .hamburger-button {
        background: none;
        border: none;
        cursor: pointer;
        position: absolute;
        transform: translate3d(-100%, -50%, 0);

        &.menu-open {
            & + nav {
                grid-template-rows: 1fr;
                opacity: 1;
            }
        }

        span {
            background: var(--violet-gray);
            border: none;
            display: block;
            height: 4px;
            width: 25px;

            &.middle-bar {
                margin: 5px 0;
            }
        }
    }

    nav {
        background: var(--violet);
        border-radius: 10px;
        display: grid;
        grid-template-rows: 0fr;
        opacity: 0;
        padding: 30px;
        position: absolute;
        right: 0;
        top: 0;
        transform: translate3d(-50px, 100px, 0);
        transition: all ease 0.4s;
        width: 50%;
        z-index: 5;

        ul {
            overflow: hidden;
            padding: 0;

            &:first-of-type {
                li {
                    padding-bottom: 20px;
                }
            }

            &:last-of-type {
                border-top: 1px solid rgba(255, 255, 255, 0.2);

                li {
                    padding-top: 20px;
                }
            }
        }

        li {
            color: #fff;
            font-size: 16px;
            font-weight: 700;
            list-style: none;
            text-align: center;

            &:hover {
                li, button {
                    color: #fff;
                }
            }

            button {
                color: #fff;
            }
        }
    }

    // media queries 
    // 600px and below 
    @media only screen and (max-width: 600px) {
        nav {
             transform: translate3d(-30px, 100px, 0);
        }
    }

    // 480px and below 
    @media only screen and (max-width: 480px) {
        nav {
            width: calc(100% - 60px);

            button {
                width: 100%;
            }
        }
    }
</style>