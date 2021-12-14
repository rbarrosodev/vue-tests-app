<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light fixed-top">
    <div class="container-fluid">
      <a class="navbar-brand" href="#">Navbar scroll</a>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarScroll" aria-controls="navbarScroll" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarScroll">
        <ul class="navbar-nav me-auto my-2 my-lg-0 navbar-nav-scroll" style="--bs-scroll-height: 100px;">
          <li class="nav-item">
            <a class="nav-link active" aria-current="page" href="#">Home</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">Link</a>
          </li>
          <li class="nav-item dropdown">
            <a class="nav-link dropdown-toggle" href="#" id="navbarScrollingDropdown" role="button" data-bs-toggle="dropdown" aria-expanded="false">
              Link
            </a>
            <ul class="dropdown-menu" aria-labelledby="navbarScrollingDropdown">
              <li><a class="dropdown-item" href="#">Action</a></li>
              <li><a class="dropdown-item" href="#">Another action</a></li>
              <li><hr class="dropdown-divider"></li>
              <li><a class="dropdown-item" href="#">Something else here</a></li>
            </ul>
          </li>
          <li class="nav-item">
            <a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Link</a>
          </li>
        </ul>
        <div class="ms-auto">
            <li class="nav-item dropdown" style="list-style-type: none;">
                <a class="nav-link dropdown-toggle" href="#" id="navbarScrollingDropdown" role="button" data-bs-toggle="dropdown" aria-expanded="false" >
                  Welcome {{ this.name }}
                </a>
                <ul class="dropdown-menu" aria-labelledby="navbarScrollingDropdown">
                  <li><a class="dropdown-item" @click="scrollToElement">Action</a></li>
                </ul>
              </li>
        </div>
      </div>
    </div>
  </nav>
  <Weather/>
  <UserMenu @teste="updateNav"/>
  <QuizParent/>
  <News/>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import Weather from './components/Weather.vue';
import UserMenu from './components/UserMenu.vue';
import UserNavbar from './components/UserNavbar.vue';
import QuizParent from './components/QuizParent.vue';
import News from './components/News.vue';

@Options({
  components: {
    Weather,
    UserMenu,
    UserNavbar,
    QuizParent,
    News,
  },
})

export default class App extends Vue {
  name = "";

  async mounted(){
      this.updateNav();
  }

  async updateNav(){
      const response = await this.axios.get(`http://localhost:3000/users/1.json`);
      this.name = response.data.name;
      this.name = this.name.split(' ')[0]
  }
}
  
</script>

<style>
#app {
  font-family: Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
