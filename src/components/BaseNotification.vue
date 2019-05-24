<template>
    <div class="notification">
        <h2 v-if="header">{{ header }}</h2>
        <p>{{ content }}</p>
    </div>
</template>

<script>
export default {
    props: {
        header: {
            type: String,
            required: false
        },
        content: {
            type: String,
            required: true
        }
    }
}
</script>

<style lang="scss" scoped>
    .notification {
        background: white;
        border-radius: 8px;
        box-shadow: 2px 2px 8px transparentize(black, 0.9);
        padding: 48px;

        h2 {
            margin-top: 0;
        }
    }
</style>
