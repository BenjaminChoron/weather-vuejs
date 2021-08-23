<template>
    <div class="container"></div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'Weather',
    data(){
        return {
            request: '',
            weather: undefined,
            api_key: process.env.VUE_APP_API_KEY,
            search_url: 'https://api.openweathermap.org/data/2.5/weather?'
        }
    },
    methods: {
        getWeather(event) {
            if(event.key == "Enter") {
                axios
                .get(`${this.search_url}q=${this.request}&units=metric&appid=${this.api_key}&lang=fr`)
                .then(response => {
                    this.weather = response.data
                    console.log(this.weather);
                })
                this.request = '';
            }
        },
        getWeatherClick() {
            axios
            .get(`${this.search_url}q=${this.request}&units=metric&appid=${this.api_key}&lang=fr`)
            .then(response => {
                this.weather = response.data
                console.log(this.weather);
            })
            this.request = '';
        }
    }
}
</script>

<style>

</style>