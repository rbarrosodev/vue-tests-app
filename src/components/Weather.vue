<template>
  <div class="hello" style="margin-top: 100px;">
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
    city = "";
    date = "";
    temp = "";
    condition = "";

    async mounted(){
        this.loadDefault();
    }


    async loadDefault(){
        const response = await this.axios.get(`http://api.weatherapi.com/v1/current.json?key=074080b14dd9472186e191951210112&q=Niteroi&aqi=no`);
        this.city = response.data.location.name;
        this.date = response.data.location.localtime;
        this.temp = response.data.current.temp_c;
        this.condition = response.data.current.condition.text;
        document.getElementById('condition-image').setAttribute( 'src', response.data.current.condition.icon );
    }

    async getWeather(param: WeatherData){
        console.log("Todo", param);

        const response = await this.axios.get(`http://api.weatherapi.com/v1/current.json?key=074080b14dd9472186e191951210112&q=${param.city}&aqi=no`)
        .catch(function (error) {
            alert("Cidade não encontrada!");
        });
        if(response){
            console.log(response.data);
            this.city = response.data.location.name;
            this.date = response.data.location.localtime;
            this.temp = response.data.current.temp_c;
            this.condition = response.data.current.condition.text;
            document.getElementById('condition-image').setAttribute( 'src', response.data.current.condition.icon );
        }
    }
}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
