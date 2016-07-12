
<style>

</style>

<template>
  <div class="dialog-container dialog-container--visible" v-show="isvisible">
    <div class="dialog">
      <div class="dialog-title">{{ msg }}</div>
      <div class="dialog-body">
        <select id="selectCityToAdd" v-model="selected">
          <option value="wheather">Wheather</option>
          <option value="cpu">CPU</option>
        </select>
      </div>
      <div class="dialog-buttons">
        <button id="butAddCity" class="button" v-on:click="triggerOpenapp">Add</button>
        <button id="butAddCancel" class="button" v-on:click="toggleisvisible">Cancel</button>
      </div>
    </div>
  </div>

</template>

<script>
export default {
  props: ['isvisible','onopenapp'],
  data () {
    return {
      msg: 'Select',
      selected: 'wheather'
    }
  },
  methods: {
    toggleisvisible: function () {    
      this.isvisible =!this.isvisible; 
      //console.warn( this.isvisible );     
    },
    triggerOpenapp: function () {           
      this.onopenapp(this.selected);     
      this.isvisible = false;
    },

  }
}
</script>

