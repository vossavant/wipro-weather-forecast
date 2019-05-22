<template>
    <article>
        <h1>{{ dt_txt }}</h1>
        <p>Main stuff:</p>
        {{ main }}
    </article>
</template>

<script>
export default {
    props: {
        dt_txt: {
            type: String
        },
        main: {
            type: Object
        }
    }
}
</script>

<style lang="scss" scoped>
    article {
        background: #feffff;
        background: -moz-linear-gradient(-45deg,  #feffff 0%, #d2ebf9 100%);
        background: -webkit-linear-gradient(-45deg,  #feffff 0%,#d2ebf9 100%);
        background: linear-gradient(135deg,  #feffff 0%,#d2ebf9 100%);
        filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#feffff', endColorstr='#d2ebf9',GradientType=1 );
        border: 1px solid #ccc;
        border-radius: 4px;
        max-width: 19%;
        padding: 20px;
    }
</style>
