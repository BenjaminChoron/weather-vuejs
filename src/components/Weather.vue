<template>
    <div class="container">
        <h1 class="my-4 text-center">
            <img src="../assets/weather.svg" alt="weather" style="width: 50px">
            Météo
        </h1>

        <div class="form-group mb-5 text-center">
            <label class="mb-2" for="position">Entrez le nom d'une ville</label>
            <input 
                type="text" 
                name="position" 
                id="position"
                class="form-control"
                v-model="request"
                v-on:keypress="getWeather"
            >
            <button class="btn btn-warning mt-3" v-on:click="getWeatherClick">Recherche</button>
        </div>

        <div class="card text-center mb-3" style="width: 18rem;" v-if="weather">
            <div class="card-body">
                <h5 class="card-title mb-4 bg-dark text-light rounded p-1">
                    <img src="../assets/placeholder.svg" alt="location" class="icon">
                    {{ weather.name.toUpperCase() }}
                </h5>

                <p class="card-text">
                    {{ Math.round(weather.main.temp*10)/10 }}
                    <img src="../assets/thermometer.svg" alt="temperature" class="icon">
                </p>

                <p class="card-text">
                    {{ weather.weather[0].description }}
                    <img :src="`http://openweathermap.org/img/wn/${weather.weather[0].icon}.png`">
                </p>

                <p class="card-text">
                    {{ $moment((weather.sys.sunrise + weather.timezone) * 1000).format('HH:mm:ss') }}
                    <img src="../assets/dawn.svg" alt="sunrise" class="icon">
                </p>

                <p class="card-text">
                    {{ $moment((weather.sys.sunset + weather.timezone) * 1000).format('HH:mm:ss') }}
                    <img src="../assets/sunset.svg" alt="sunset" class="icon">
                </p>
            </div>
        </div>
    </div>
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
h1, label {
    color: whitesmoke;
}
.icon {
    width: 30px;
    margin: .4rem;
}
</style>