
<template>

  <div class="panel" >
      <span> Додавання міста  </span>
        <input type = "text" v-model = "newCity">
        <button class = "btn btn-send" v-on:click = "add()">Додати</button><br>
        <span> Вибір міста </span>
        <select v-model = "city">
            <option v-for="item in cityArr" v-bind:key="item">{{ item }}</option>
        </select><br>
        <button class = "btn btn-send" v-on:click = "getWeather()">Погода</button>

        
<div class="card">
       
        <br>
         <h2>{{info.name}}</h2>
        
        <br>
        <h2>{{info.main.temp}}</h2>
        <br>
        <h3>Wind speed{{ info.wind.speed}}mph</h3>
        
        
          
        <table>
            <tr>
                <td>Min t</td>
                <td>Max t</td>
                <td>Wind t</td>
                
            </tr>
            <tr>
                <td>{{info.main.temp_min}} °C</td>
                <td>{{info.main.temp_max}} °C</td>
                <td>{{info.wind.deg}} °C</td>
               
            </tr>
            
        </table>

        
    </div>
    </div>
  
  
</template>

<style>
.panel{
    margin-right: auto;
    margin-left: auto;
    background: url(wind.png);
    width: 500px;
        color: aliceblue;
}
.btn-send{
    color: aliceblue;
    font-weight:bold;
        text-shadow:black 1px 1px 0, black -1px -1px 0, 
                 black -1px 1px 0, black 1px -1px 0;
}

h3{
    color: bisque;
        text-shadow:black 1px 1px 0, black -1px -1px 0, 
                 black -1px 1px 0, black 1px -1px 0;
}
.card{
    background: url(w.png);
    color: aliceblue;
    text-shadow:black 1px 1px 0, black -1px -1px 0, 
                 black -1px 1px 0, black 1px -1px 0;
}
</style>


<script>
import axios from 'axios'


export default {
 data: function() {
   return{
        info: null,
         city:'',
               newCity:"",
               cityArr: ["Seul","Osaka"],
               latitude:"47",
               longitude:"35",
               Seul:"Seul",
                myCoordinates: {
                    lat: 0,
                    lng: 0
                },
               
   }
  },
  mounted: function(){
      this.getCord()
            axios.get("https://api.openweathermap.org/data/2.5/weather?lat="+this.myCoordinates.lat+"&lon="+this.myCoordinates.lng+"&appid=dcb16dd01cccb18cd312750106a9ed04").then((response) =>{
                console.log(response.data);
                console.log(this.myCoordinates.lat);
                console.log(this.myCoordinates.lng);
                this.info = response.data;
            })
           
            },
             methods: {
             getWeather:function(){
               axios.get("https://api.openweathermap.org/data/2.5/weather?q=" + this.city + ",&appid=dcb16dd01cccb18cd312750106a9ed04").then((response) =>{
                    console.log(response.data);
                    this.info = response.data;
                })
            },
            add:function(){
                this.cityArr.push(this.newCity)
            },
            getCord: function () {
                 this.$getLocation({})
                    .then(coordinates => {
                        this.myCoordinates = coordinates;
                    })
                    .catch(error => alert(error));
                         axios.get("https://api.openweathermap.org/data/2.5/weather?lat="+this.myCoordinates.lat+"&lon="+this.myCoordinates.lng+"&appid=dcb16dd01cccb18cd312750106a9ed04").then((response) =>{
                console.log(response.data);
                console.log(this.myCoordinates.lat);
                console.log(this.myCoordinates.lng);
                this.info = response.data;
            })
                    
            },
         
          

        
        },
             
        }
</script>
<style scoped>

</style>
