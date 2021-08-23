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
                v-on:keypress="goMeteo"
            >
            <button class="btn btn-warning mt-3" v-on:click="goMeteoClick">Recherche</button>
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