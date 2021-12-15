<template>
    <div class="card mx-auto" style="width: 40rem; margin-top: 100px;">
        <ul id="infinite-list" class="list-group list-group-flush">
            <li class="list-group-item" v-for="item in titles"><a :href="[item.url]" style="text-decoration: none;" target="_blank">{{ item.title }}</a></li>
        </ul>
    </div>
</template>

<script>
    import { Options, Vue } from 'vue-class-component';

    @Options({})
    export default class News extends Vue {
        titles = [];
        page = 1;

        async mounted(){
             window.onscroll = () => {
                let bottomOfWindow = document.documentElement.scrollTop + window.innerHeight === document.documentElement.offsetHeight;
                if (bottomOfWindow) {
                    this.page++;
                    this.getNewNews();
                }
            };
            this.getNewNews();
        }

        getNewNews() {
            this.axios.get(`https://newsapi.org/v2/top-headlines?country=br&pagesize=5&page=${this.page}&apiKey=b180df5ee2984fbdafde4c5b1fe6958b`).then(response => {
                for(var i in response.data.articles){
                    this.titles.push(response.data.articles[i]);
                }
            });
        }
    }
</script>

<style scoped>

</style>