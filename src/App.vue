<template>
<div class="app ">
  <div class="header container h-full p-12   max-w-5xl mx-auto">
    <h1 class="mb-5 text-3xl font-bold text-center">Weather App</h1>
    <div class="flex justify-center h-full text-center ">
      <div class="searchbar  ">
        <input type="text" class="input form-control w-96 mx-2 rounded h-8 text-black" v-model="city" placeholder="Search for a city...">
      </div>
      <button
        class="btn-search inline-block align-middle text-center select-none border 
        font-normal whitespace-nowrap rounded py-0 px-2 leading-normal no-underline
       bg-blue-500 text-white hover:bg-blue-600" @click="SearchWeather">Search <i class="fa-solid fa-magnifying-glass"></i>
      </button>
    </div>
  </div>
  <!--====Define the Weather Component Start====-->
  <Weather :city="city" v-if="showWeather"></Weather>
  <!--====Define the Weather Component End====-->
</div>

</template>

<script>
import Weather from './components/Weather.vue';

export default {
  name: 'App',
  components: { 
    Weather  
  },
  data(){
    return{
      city:'',
      showWeather: false,
    }
  },
  //when user search weather this method will works to showWeather start
  methods: {
    async SearchWeather(){
      this.showWeather = false
      await this.$nextTick();
      this.showWeather = true
    }
  }
  //when user search weather this method will works to showWeather start

}
</script>

<style>

body{
  background-color: #121212 !important;
}
.header{
  background-color: #212730;
  border-radius: 1.2rem;
  color: #fff;
  text-align: center;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  margin-top: 5rem;
}
.btn-search{
  background-image: linear-gradient(to right, cyan, magenta);
}




</style>
