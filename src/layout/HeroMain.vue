<script setup>
    import ButtonMain from './../components/ButtonMain.vue'; 
</script>

<template>
    <section class="hero">
        <div class="section-header" v-show="$slots.title || $slots.subtitle">
            <h1><slot name="title"></slot></h1>
            <p><slot name="subtitle"></slot></p>
            <ButtonMain>Get Started</ButtonMain>
        </div>
        <div class="section-image">
            <img src="./../../images/illustration-working.svg" alt="Cartoon illustration of a person sitting and working at desk." />
        </div>
    </section>
</template>

<style scoped lang="scss">
    .hero {
        align-items: center;
        display: flex;
        margin-bottom: 100px;

        .section-header {
            flex-basis: 50%;
            flex-shrink: 0;
            padding-right: 25px;

            h1 {
                line-height: 1.2;
            }
        }

        .section-image {
            flex-basis: 50%;
        }
    }

    // media queries 
    // 800px
    @media only screen and (max-width: 800px) {
        .hero {
            flex-direction: column-reverse;

            .section-header {
                padding-right: 0;
                text-align: center;

                p {
                    margin: 30px 0;
                }
            }
            
            .section-image {
                margin-bottom: 50px;

                img {
                    transform: translate3d(10vw, 0, 0);
                    width: 100vw;
                }
            }
        }
    }
</style>