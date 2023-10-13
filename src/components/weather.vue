<!-- eslint-disable vue/multi-word-component-names -->
<template>
    <div class="container">
        <div class="innercontainer">
            <h2>{{ temperature }}<span>&#176;</span></h2>
            <p>{{ weatherDescription }}</p>

            <div v-if="showCloudy" class="weather-condition">
                <img src="../assets/cloudy.png" alt="">
            </div>
            <div v-if="showRainy" class="weather-condition">
                <img src="../assets/rain.png" alt="">
            </div>
            <div v-if="showStormy" class="weather-condition">
                <img src="../assets/storm.png" alt="">
            </div>
            <div v-if="showClear" class="weather-condition">
                <img src="../assets/clear.png" alt="">
            </div>
            <div v-if="showDrizzle" class="weather-condition">
                <img src="../assets/drizzle.png" alt="">
            </div>
            <div v-if="showSnow" class="weather-condition">
                <img src="../assets/snow.png" alt="">
            </div>
            <div v-if="showAtmosphere" class="weather-condition">
                <img src="../assets/atmosphere.png" alt="">
            </div>

            <div class="input-container">
                <label for="latitude">Latitude</label>__
                <input type="text" name="latitude" v-model="latitude">
            </div>
            <div class="input-container">
                <label for="longitude">Longitude</label>_
                <input type="text" name="longitude" v-model="longitude">
            </div>
            <br>
            <button @click="GetWeatherData()" class="Ca1"><img src="../assets/search.png" alt=""></button>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
    export default {
        data(){
            return{
                weather:{},
                weatherDescription: '',
                showCloudy: false,
                showRainy: false,
                showStormy: false,
                showClear: false,
                showDrizzle: false,
                showSnow: false,
                showAtmosphere: false,
                temperature: '',
                latitude: '18.7965',
                longitude: '98.6601'
            }   

        },
    methods:{
        GetWeatherData(){
            axios.get('https://api.openweathermap.org/data/2.5/weather?lat='+ this.latitude +'&lon='+ this.longitude +'&appid=a41d8d352d1ca4528378c092b970ce3c').then(
                response => {
                    console.log(response.data.weather)
                    let mainDescription = response.data.weather[0].main;
                    let descriptionString = response.data.weather[0].description;
                    this.weatherDescription = descriptionString.charAt(0).toUpperCase() + descriptionString.slice(1);
                    
                    this.temperature = response.data.main.temp;

                    switch(true){
                        case mainDescription == 'Clouds':
                            this.showCloudy = true;
                            this.showStormy = false;
                            this.showRainy = false;
                            this.showClear = false;
                            this.showDrizzle = false;
                            this.showSnow = false;
                            this.showAtmosphere = false;
                            break;
                        case mainDescription == 'Thunderstorm':
                            this.showCloudy = false;
                            this.showStormy = true;
                            this.showRainy = false;
                            this.showClear = false;
                            this.showDrizzle = false;
                            this.showSnow = false;
                            this.showAtmosphere = false;
                            break;
                        case mainDescription == 'Rain':
                            this.showCloudy = false;
                            this.showStormy = false;
                            this.showRainy = true;
                            this.showClear = false;
                            this.showDrizzle = false;
                            this.showSnow = false;
                            this.showAtmosphere = false;
                            break;
                        case mainDescription == 'Clear':
                            this.showCloudy = false;
                            this.showStormy = false;
                            this.showRainy = false;
                            this.showClear = true;
                            this.showDrizzle = false;
                            this.showSnow = false;
                            this.showAtmosphere = false;
                            break;
                        case mainDescription == 'Drizzle':
                            this.showCloudy = false;
                            this.showStormy = false;
                            this.showRainy = false;
                            this.showClear = false;
                            this.showDrizzle = true;
                            this.showSnow = false;
                            this.showAtmosphere = false;
                            break;
                        case mainDescription == 'Snow':
                            this.showCloudy = false;
                            this.showStormy = false;
                            this.showRainy = false;
                            this.showClear = false;
                            this.showDrizzle = false;
                            this.showSnow = true;
                            this.showAtmosphere = false;
                            break;
                        case mainDescription == 'Atmosphere':
                            this.showCloudy = false;
                            this.showStormy = false;
                            this.showRainy = false;
                            this.showClear = false;
                            this.showDrizzle = false;
                            this.showSnow = false;
                            this.showAtmosphere = true;
                            break;
                    }
                }
            ).catch(error => {console.log(error)})
        }
    },
    mounted(){
        this.GetWeatherData();
    }
}
</script>

<style>
.container {
    width: 100%;
    display: flex;
    justify-content: center;
}

.innercontainer {
    max-width: 470px;
    background: linear-gradient(135deg, #00feba , #5b548a);
    color: #fff;
    margin: 100px auto 0;
    border-radius: 50%;
    width: 60%;
    height: 60%;
    padding: 40px 35px;
    text-align: center;
    border: 0;
    outline: 0;
    
}

.Ca1 img {    
    width: 16px;

}
.Ca1{
    border: 0;
    outline: 0;
    background: #ebfffc;
    border-radius: 50%;
    width: 60px;
    height: 60px;
    cursor: pointer;
}

h2{
    font-size: 70px;
}

</style>