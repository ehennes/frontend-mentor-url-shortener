<template>
    <section>
        <div class="section-header" v-show="$slots.title || $slots.subtitle">
            <h2><slot name="title"></slot></h2>
            <p><slot name="subtitle"></slot></p>
        </div>
        <div class="section-content" v-show="$slots.content">
            <slot name="content"></slot>
        </div>
    </section>
</template>

<style scoped lang="scss">
    .section-header {
        margin: 0 auto;
        max-width: 45ch;

        h2, p {
            text-align: center;
        }
    }
</style>