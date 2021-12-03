<template>
    <div class="user-menu">
        <div class="col-md-3 mx-auto">
            <div class="card" style="width: 30rem;">
                <div class="card-body" id="cardInfo">
                    <h5 class="card-title">{{ this.name }}</h5>
                    <p class="card-text">{{ this.email }}</p>
                    <p class="card-text">{{ this.birthday }}</p>
                    <p class="card-text">{{ this.city }}</p>
                    <button class="btn btn-primary mt-2" @click="openForm()">Editar</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
    import { Options, Vue } from 'vue-class-component';

    @Options({})
    export default class UserMenu extends Vue {
        name = "";
        email = "";
        birthday = "";
        city = "";

        userFormInput = { name: "", email: "", birthday: "", city: "" };

        async mounted(){
            this.loadDefaultUser();
        }

        async loadDefaultUser(){
            const response = await this.axios.get(`http://localhost:3000/users/1.json`);
            this.name = response.data.name;
            this.email = response.data.email;
            this.birthday = response.data.birthday;
            this.city = response.data.city;
        }

        async completeForm(){
            this.userFormInput.name = this.name;
            this.userFormInput.email = this.email;
            this.userFormInput.birthday = this.birthday;
            this.userFormInput.city = this.city;
        }

        async onSubmit(){
            console.log('enviou');

            await this.axios.put(`http://localhost:3000/users/1.json`, {
                name: this.userFormInput.name,
                email: this.userFormInput.email,
                birthday: this.userFormInput.birthday,
                city: this.userFormInput.city
            });
            this.loadDefaultUser();

            this.userFormInput.name = "";
            this.userFormInput.email = "";
            this.userFormInput.birthday = "";
            this.userFormInput.city = "";

            this.$emit("teste", this.userFormInput);
        }

        async openForm(){
            var card = document.getElementById('cardInfo');
            card.innerHTML = `<form @submit.prevent :model="userFormInput" class="form-input">
                                <div class="form-group">
                                    <label for="formGroupExampleInput" prop="name">Nome:</label>
                                    <input type="text" class="form-control mt-2" id="formGroupExampleInput" v-model="userFormInput.name" placeholder="Insira seu nome">
                                </div>
                                <div class="form-group">
                                    <label for="formGroupExampleInput" prop="email">Email:</label>
                                    <input type="text" class="form-control mt-2" id="formGroupExampleInput" v-model="userFormInput.email" placeholder="Insira seu email">
                                </div>
                                <div class="form-group">
                                    <label for="formGroupExampleInput" prop="birthday">Aniversário:</label>
                                    <input type="text" class="form-control mt-2" id="formGroupExampleInput" v-model="userFormInput.birthday" placeholder="Insira seu aniversário">
                                </div>
                                <div class="form-group">
                                    <label for="formGroupExampleInput" prop="city">Cidade:</label>
                                    <input type="text" class="form-control mt-2" id="formGroupExampleInput" v-model="userFormInput.city" placeholder="Insira sua cidade">
                                </div>
                
                                <button class="btn btn-primary mt-2" @click="onSubmit()">Enviar</button>
                            </form>`
        }
    }
</script>

<style>
    .user-menu {
        margin-top: 100px;
    }
</style>