
<style>

</style>

<template>
     <header class="headerapp cardTemplate">
         <h1 class="headerapp__title">{{msg}}</h1>
         <button id="butRefresh" class="headerButton" aria-label="Refresh" v-on:click="getForecast"></button>
         <button id="butClose" class="headerButton" aria-label="Close"  v-on:click="triggerclose" > </button>
    </header> 
     <div class="card cardTemplate weather-forecast" >


     
      <div class="city-key" ></div>
      <div class="location"> {{forecast.name}} </div>

<!-- <pre>@{{ $data | json }}</pre> -->
      
      <div class="date"> {{forecasttimestamp}}  </div>
      <div class="description">{{forecast.weather[0].description}}</div>
      <div class="current">
        <div class="visual">
          <div class="icon"><a href="http://www.buienradar.nl/weer/Haarlem/NL/2755003#overzicht"><img v-bind:src="geticonurl" /> </a></div>
          <div class="temperature">
            <span class="value"> {{forecast.main.temp}} </span><span class="scale">°C</span>
          </div>
        </div>
        <div class="description">
          <div class="feels-like">
            <span class="value"></span><span class="scale">°F</span>
          </div>
          <div class="precip"></div>
          <div class="humidity">{{forecast.main.humidity}}%</div>
          <div class="wind">
            <span class="value"></span>
            <span class="scale">{{forecast.wind.speed}} mph</span>
            <span class="direction">{{forecast.wind.deg}}</span>°
          </div>
        </div>
      </div>
      <!--
      <div class="future">
        <div class="oneday">
          <div class="date"></div>
          <div class="icon"></div>
          <div class="temp-high">
            <span class="value"></span>°
          </div>
          <div class="temp-low">
            <span class="value"></span>°
          </div>
        </div>
        <div class="oneday">
          <div class="date"></div>
          <div class="icon"></div>
          <div class="temp-high">
            <span class="value"></span>°
          </div>
          <div class="temp-low">
            <span class="value"></span>°
          </div>
        </div>
        <div class="oneday">
          <div class="date"></div>
          <div class="icon"></div>
          <div class="temp-high">
            <span class="value"></span>°
          </div>
          <div class="temp-low">
            <span class="value"></span>°
          </div>
        </div>
        <div class="oneday">
          <div class="date"></div>
          <div class="icon"></div>
          <div class="temp-high">
            <span class="value"></span>°
          </div>
          <div class="temp-low">
            <span class="value"></span>°
          </div>
        </div>
        <div class="oneday">
          <div class="date"></div>
          <div class="icon"></div>
          <div class="temp-high">
            <span class="value"></span>°
          </div>
          <div class="temp-low">
            <span class="value"></span>°
          </div>
        </div>
        <div class="oneday">
          <div class="date"></div>
          <div class="icon"></div>
          <div class="temp-high">
            <span class="value"></span>°
          </div>
          <div class="temp-low">
            <span class="value"></span>°
          </div>
        </div>
        <div class="oneday">
          <div class="date"></div>
          <div class="icon"></div>
          <div class="temp-high">
            <span class="value"></span>°
          </div>
          <div class="temp-low">
            <span class="value"></span>°
          </div>
        </div>
      </div>
      -->
    </div>
    
</template>

<script>
//http://stackoverflow.com/questions/847185/convert-a-unix-timestamp-to-time-in-javascript
export
default {
  props: ['isvisible', 'methodclose', 'appcfg'],
  data() {
    return {
      msg: 'Current weather',
      forecast : {"coord":{"lon":4.64,"lat":52.38},"weather":[{"id":801,"main":"Clouds","description":"licht bewolkt","icon":"02d"}],"base":"cmc stations","main":{"temp":20.61,"pressure":1009,"humidity":56,"temp_min":18.33,"temp_max":23.33},"wind":{"speed":11.8,"deg":230},"clouds":{"all":20},"dt":1468258380,"sys":{"type":1,"id":5204,"message":0.0043,"country":"NL","sunrise":1468208039,"sunset":1468267171},"id":2755003,"name":"Haarlem","cod":200}
    }
  },
  ready: function () {
    console.log('ready to LookAtTheWeather');
    this.getForecast();
    this.LookAtTheWeather();
  },
  computed: {
    geticonurl: function() {
      return 'http://openweathermap.org/img/w/' + this.forecast.weather[0].icon + '.png';
    },
    forecasttimestamp: function() {
    /*
      // Create a new JavaScript Date object based on the timestamp
      // multiplied by 1000 so that the argument is in milliseconds, not seconds.
      var date = new Date(this.forecast.dt*1000);
      // Hours part from the timestamp
      var hours = date.getHours();
      // Minutes part from the timestamp
      var minutes = '0' + date.getMinutes();
      // Seconds part from the timestamp
      var seconds = '0' + date.getSeconds();

      // Will display time in 10:30:23 format
      return hours + ':' + minutes.substr(-2) + ':' + seconds.substr(-2);
      */
      var a = new Date(this.forecast.dt*1000);
      var months = ['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];
      var year = a.getFullYear();
      var month = months[a.getMonth()];
      var date = a.getDate();
      var hour = a.getHours();
      var min = a.getMinutes();
      var sec = a.getSeconds();
      var time = date + ' ' + month + ' ' + year + ' ' + hour + ':' + min + ':' + sec ;
      return time;
    } 
  },
  methods: {
    toggleisvisible: function() {
      this.isvisible = !this.isvisible;
    },
    triggerclose: function() {
      console.log('tc');
      this.methodclose(this);
    },
    // Gets a forecast for a specific city and update the card with the data
    getForecast: function(key, label) {
      var url = 'http://api.openweathermap.org/data/2.5/weather?q=Haarlem,NL&units=metric&lang=nl&APPID=32de1cbe64c27cc20a71f3561f13bb1f'
      //var url = 'https://publicdata-weather.firebaseio.com/';
      //url += key + '.json';
      // Make the XHR to get the data, then update the card
      var self = this;
      var request = new XMLHttpRequest();
      request.onreadystatechange = function() {
        if (request.readyState === XMLHttpRequest.DONE) {
          if (request.status === 200) {
            var response = JSON.parse(request.response);
            //response.key = key;
            //response.label = label;
            //app.updateForecastCard(response);
            console.warn(response);
            self.forecast = response;
          }
        }
      };
      request.open('GET', url);
      request.send();
    },
    LookAtTheWeather: function() {
      var self = this;
      self.getForecast()
      var t = setTimeout(self.LookAtTheWeather, 10*60*1000);
    }
  }
}
</script>

