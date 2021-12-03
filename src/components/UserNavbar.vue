<template>
</template>

<script lang="ts">
    import { Options, Vue } from 'vue-class-component';

    @Options({
        props: {
            msg: String
        }
    })
    export default class UserNavbar extends Vue {
        async mounted(){
            this.$emit("testing");
        }

        async loadUser(){
            const response = await this.axios.get(`http://localhost:3000/users/1.json`);
            this.msg = response.data.name;
        }
    }
</script>