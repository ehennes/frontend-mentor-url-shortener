<script setup>

</script>

<template>
    <div class="card">
        <div class="card-header">
            <div class="card-icon">
                <slot name="icon"></slot>
            </div>
            <div class="card-title">
                <h3><slot name="title"></slot></h3>
            </div>
        </div>
        <div class="card-content">
            <p><slot name="content"></slot></p>
        </div>
    </div>
</template>

<style lang="scss">
    .card {
        background: #fff;
        border-radius: 5px;
        padding: 0 3% 3%;

        &:nth-of-type(2) {
            transform: translate3d(0, 35px, 0);
        }

        &:nth-of-type(3) {
            transform: translate3d(0, 70px, 0);
        }

        .card-header {
            .card-icon {
                align-items: center;
                background: var(--violet);
                border-radius: 100%;
                display: flex;
                height: 70px;
                justify-content: center;
                transform: translate3d(0, -50%, 0);
                width: 70px;

                svg {
                    transform: scale(0.8);
                }
            }
        }
    }

    @media only screen and (max-width: 800px) {
        .card {
            padding: 0 30px 30px;

            &:not(:last-of-type) {
                margin-bottom: 50px;
            }

            .card-header {
                .card-icon {
                    margin: 0 auto;
                }

                .card-title {
                    h3 {
                        text-align: center;
                    }
                }
            }

            .card-content {
                p {
                    text-align: center;
                }
            }
        }
    }
</style>