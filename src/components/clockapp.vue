
<style>

</style>

<template>
    
     <header class="headerapp cardTemplate">
         <h1 class="headerapp__title">{{msg}}</h1>
         <button id="butClose" class="headerButton" aria-label="Close"  v-on:click="triggerclose" > </button>
    </header> 

    <div class="card cardTemplate weather-forecast" >
       <h2> {{msg}} {{currenttime}}</h2>
    </div>
    
</template>

<script>
export
default {
  props: ['isvisible', 'methodclose', 'appcfg'],
  data() {
    return {
      msg: 'Current time',
      currenttime : '12'
      }
  },
  computed: {
  },
  ready: function () {
    console.log('ready ');
    this.LookAtTheTime();
  },
  methods: {
    toggleisvisible: function() {
      this.isvisible = !this.isvisible;
    },
    triggerclose: function() {
      //console.log('tc');
      this.methodclose(this);
    },
    checkTime: function(i) {
      if (i < 10) {
        i = "0" + i;
      }
      return i;
    },
    gettimehr: function() {
      var self = this;
      var today = new Date();
      var h = today.getHours();
      var m = today.getMinutes();
      var s = today.getSeconds();
      // add a zero in front of numbers<10
      m = self.checkTime(m);
      s = self.checkTime(s);
      var time = " "+h + ":" + m + ":" + s
      //console.info(time);
      //console.info(s);
      //console.info(self.currenttime);
      self.currenttime=(time);
      //this.LookAtTheTime();
      //return time;
    },
    LookAtTheTime: function() {
      var self = this;
      self.gettimehr()
      var t = setTimeout(self.LookAtTheTime, 900);
    }
  }
}
</script>

