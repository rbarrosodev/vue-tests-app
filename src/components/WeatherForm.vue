<template>
    <form @submit.prevent :model="formInput" class="form-input">
        <div class="form-group">
          <label for="formGroupExampleInput" prop="city">Insira sua cidade:</label>
          <input type="text" class="form-control mt-2" id="formGroupExampleInput" v-model="formInput.city" placeholder="Insira sua cidade">
          <button class="btn btn-primary mt-2" @click="onSubmit()">Enviar</button>
        </div>
    </form>
</template>

<script>
    import { Options, Vue } from 'vue-class-component';

    @Options({})
    export default class WeatherForm extends Vue {
        formInput = { city: "" };

        onSubmit(){
            this.$emit('send-form', this.formInput);
            this.formInput.city = "";
        }
    }
</script>