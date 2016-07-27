
<style>

</style>

<template>
    
     <header class="headerapp cardTemplate">
         <h1 class="headerapp__title">{{msg}}</h1>
         <button id="butClose" class="headerButton" aria-label="Close"  v-on:click="triggerclose" > </button>
    </header> 

    <div class="card cardTemplate weather-forecast" >
       <h2> {{msg}} </h2>
       <gcse:search></gcse:search>
    </div>
    
</template>

<script>
export
default {
  props: ['isvisible', 'methodclose', 'appcfg'],
  data() {
    return {
      msg: 'Google site search'
      }
  },
  computed: {
  },
  ready: function () {
    console.log('ready ');
    var cx = '008673413979122676695:urshifhqjoe';
    var gcse = document.createElement('script');
    gcse.type = 'text/javascript';
    gcse.async = true;
    gcse.src = 'https://cse.google.com/cse.js?cx=' + cx;
    var s = document.getElementsByTagName('script')[0];
    s.parentNode.insertBefore(gcse, s);
  },
  methods: {
    toggleisvisible: function() {
      this.isvisible = !this.isvisible;
    },
    triggerclose: function() {
      console.log('tc');
      this.methodclose(this);
    }
  }
}
</script>

