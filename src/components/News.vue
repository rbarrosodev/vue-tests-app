<template>
    <div class="card mx-auto" style="width: 40rem;">
        <ul class="list-group list-group-flush">
            <li class="list-group-item" v-for="item in titles"><a :href="[item.url]" style="text-decoration: none;" target="_blank">{{ item.title }}</a></li>
        </ul>
    </div>
</template>

<script>
    import { Options, Vue } from 'vue-class-component';

    @Options({})
    export default class News extends Vue {
        titles = [];

        async beforeMount() {
            const response = await this.axios.get(`https://newsapi.org/v2/top-headlines?country=br&category=general&apiKey=18e19938a9524d4ca24792af52f27251`);
            for(var i in response.data.articles){
                this.titles.push(response.data.articles[i]);
            }
        }

        async mounted(){
            this.getNewNews();
        }

        getNewNews() {
            window.onscroll = () => {
                let bottomOfWindow = document.documentElement.scrollTop + window.innerHeight === document.documentElement.offsetHeight;
                if (bottomOfWindow) {
                this.axios.get(`https://newsapi.org/v2/top-headlines?country=br&apiKey=18e19938a9524d4ca24792af52f27251`).then(response => {
                        for(var i in response.data.articles){
                            this.titles.push(response.data.articles[i]);
                        }
                    });
                }
            }
        }
    }
</script>

<style scoped>

</style>