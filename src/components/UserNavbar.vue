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
    }
</script>