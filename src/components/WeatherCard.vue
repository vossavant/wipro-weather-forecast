<template>
    <article>
        <header>
            {{ weather[0].main }}
            {{ formattedTemp }}&deg;
        </header>
        <div class="whatever">
            <h3>{{ city.name }}, {{ city.country }}</h3>
            <p>{{ formattedMonth }} {{ formattedDate }}</p>
        </div>
        <p>{{ formattedDay }}</p>

        <h4>Temp</h4>
        <pre>{{ main }}</pre>

        <h4>Weather</h4>
        <pre>{{ weather }}</pre>
    </article>
</template>

<script>
export default {
    computed: {
        formattedDate() {
            return this.dateTime.getDate();
        },

        formattedDay() {
            return this.dateTime.toLocaleString('default', { weekday: 'short' });
        },

        formattedMonth() {
            return this.dateTime.toLocaleString('default', { month: 'long' });
        },

        formattedTemp() {
            return Math.round(this.main.temp);
        }
    },

    data() {
        return {
            dateTime: new Date(this.dt * 1000)
        }
    },

    props: {
        city: String,
        dt: {
            type: Number
        },
        main: {
            type: Object
        },
        weather: {
            type: Array
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
