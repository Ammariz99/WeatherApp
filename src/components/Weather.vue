<template>
      <!--==========Today's Weather Card Start===========-->
      <div class="container p-5 max-w-[80%]    mx-auto">
        <div class="flex">
            <div class="card main-div w-full bg-white text-white">
                <img src="@/assets/mountain-8590965_1280.jpg" class="rounded-2xl h-full" alt="" srcset="">
                <div class="absolute top-0 left-0 right-0 p-3">
                    <h1 class="day mb-1 text-xl font-bold">Today</h1>
                    <p class="date text-gray-200 mb-0 text-3xl font-normal">{{ date }}</p>
                    <small class="text-base">{{ time }}</small>
                    <h2 class="place "><i class="fa-solid fa-location-dot">{{ city }} <small>{{ country }}</small></i></h2>
                </div>
                <div class="temp absolute bottom-0 ml-24 transform -translate-x-1/2 z-10 ">
                    <h1 class="weather-temp m-0 font-bold text-4xl">{{ Math.floor( temprature) }}&deg;</h1>
                    <h2 class="text-gray-400 flex items-center">{{ description }} <img :src="iconUrl" class="ml-2"> </h2>
                </div>
                
            </div>
        <!--Card 2 inside flex div to show both cards in parallel Start-->
            <div class="card card-2 w-full  bg-[#212730] rounded-2xl">
            
            <table class="table m-6 w-5/6 ml-7  relative left-4 border-separate border-spacing-4 text-left mx-auto">
                <tbody class=" text-nowrap">
                    <tr>
                        <th>Max Temp</th>
                        <td class="w-1/2 ">{{ Math.floor(temp_max) }} &deg;</td>
                    </tr>
                    <tr>
                        <th>Humidity</th>
                        <td class="w-1/2">{{ humidity }}</td>
                    </tr>
                    <tr>
                        <th>Wind</th>
                        <td class="w-1/2">{{ wind }}</td>
                    </tr>
                    
                </tbody>
            </table>
            <!--====Define Component daysWeather Start======-->
            <daysWeather :cityName="cityName"></daysWeather>
            <!--====Define Component daysWeather End======-->
            <div class="id_form flex m-3 justify-center" id="div_form">
                <form action="">
                    <input type="button" value="Change Location" @click="changeLocation" class="btn change-btn h-8 w-36 rounded bg-gradient-to-r from-cyan-500 to-sky-500 cursor-pointer">
                </form>
            </div>
        </div> 
        <!--Card 2 inside flex div to show both cards in parallel End-->   
        </div>


        
      </div>
      <!--==========Today's Weather Card End===========-->
    
    </template>
    
    <script>
    import axios from 'axios';
    import daysWeather from './daysWeather.vue';

    export default {
  name: 'myWeather',
  components: { 
    daysWeather,
  },
  //pass the props to city string
  props: {
    city: String,
  },
  //fetch data into our components start
  data(){
    return {
        //return some variable or pass the props
        cityName: this.city,
        country: null,
        temprature: null,
        description: null,
        iconUrl: null,
        date: null,
        time: null,
        temp_max: null,
        humidity: null,
        wind: null,

        monthNames: ["January", "February", "March", "April", "May", "June", "July", "August", "September",
            "October", "November", "December"
        ]

    }
  },
  methods:{
    changeLocation(){
        window.location.reload();
    }
  },
   //fetch data into our components end

  //get the data from the api start
  async created(){
    const response = await axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=8331cdef4f10633c84fd856ce65588b0`)
    //assign these api value to props which created in data(){} above mentioned
    const weatherData = response.data;
    this.country = weatherData.sys.country;
    this.temprature = weatherData.main.temp;
    this.description = weatherData.weather[0].description;
    this.name = weatherData.name;
    this.temp_max = weatherData.main.temp_max;
    this.wind = weatherData.wind.speed;
    this.humidity = weatherData.main.humidity;
    this.iconUrl = `https://api.openweathermap.org/img/w/${weatherData.weather[0].icon}.png`;
    const d = new Date();
    this.date = d.getDate() + '-' + this.monthNames[d.getMonth()] + '-' + d.getFullYear();
    this.time = d.getHours() + ':' + d.getMinutes() + ':' + d.getSeconds();
    console.log(weatherData);
    //assign these api value to props which created in data(){} above mentioned
}
//get the data from the api end
}
    
    </script>
    
    <style>
    body{
        background-color: #343d4b;
    }
    .main-div {
    border-radius: 20px;    
    background-size:cover;
    background-position: center;
    background-blend-mode: overlay;
    position: relative;
    background-color: rgba(0, 0, 0, 0.5);
    background-repeat: no-repeat;
    }
    .main-div:hover{
        transform: scale(1.1);
        transition: transform 0.5s ease;
        z-index: 1;
    }
    
    th,td{
        font-size: 1.1rem;
        color: #fff;
    }
    td{
        text-align: right;
    }
    table, 
    tr:hover{
        color: red;
    }

    .change-btn:hover{
        transform: scale(0.9);
    }

    
    </style>
    