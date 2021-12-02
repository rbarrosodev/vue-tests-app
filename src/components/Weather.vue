<template>
  <div class="hello mt-5">
    <div class="padding">
        <div class="col-md-3 mx-auto">
            <weather-form @send-form="getWeather"></weather-form>
            <div class="card mt-3"> <img class="" src="https://i.imgur.com/a9sHoeY.jpg" alt="Card image cap">
                <div class="card-img-overlay" style="height:110px;">
                    <h3 class="card-title text-white m-b-0 dl">{{ this.city }}</h3> <small class="card-text text-white font-light">{{ this.date }}</small>
                </div>
                <div class="card-body weather-small">
                    <div class="row">
                        <div class="col-12">
                            <div class="d-flex">
                                <div class="display-6 text-info"><i class="mdi mdi-weather-pouring"></i></div>
                                <div class="m-l-20 mx-auto">
                                    <img id="condition-image">
                                    <h1 class="font-light text-info m-b-0">{{ this.temp }}<sup>0</sup></h1> <small>{{ this.condition }}</small>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import WeatherForm from './WeatherForm.vue';

interface WeatherData {
    city: string;
}

@Options({
    components: {
        WeatherForm,
    }
})

export default class Weather extends Vue {
    weather_info = [];
    city = "";
    date = "";
    temp = "";
    condition = "";
    icon_url = "";

    async mounted(){
        if(this.city.length == 0){
            this.city = "No data";
        }
    }

    async loadInfo(){
        const response = await this.axios.get(`http://api.weatherapi.com/v1/current.json?key=074080b14dd9472186e191951210112&q=Rio de Janeiro&aqi=no`);
        this.weather_info = response.data;
    }

    async getWeather(param: WeatherData){
        const response = await this.axios.get(`http://api.weatherapi.com/v1/current.json?key=074080b14dd9472186e191951210112&q=${param.city}&aqi=no`)
        .catch(function (error) {
            alert("Cidade não encontrada!");
        });
        this.weather_info = response.data;
        this.city = this.weather_info.location.name;
        this.date = this.weather_info.location.localtime;
        this.temp = this.weather_info.current.temp_c;
        this.condition = this.weather_info.current.condition.text;
        this.icon_url = "http://" + this.weather_info.current.condition.icon;
        document.getElementById('condition-image').src = this.icon_url;
        console.log(response.status);
    }
}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
