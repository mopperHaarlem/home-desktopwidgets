<template>
	<li class="list-group-item">
		<table class="row-fluid">
			<tr>
			  <td>
				<div class="onoffswitch" @click="togglecheck">
				  <input type="checkbox" name="onoffswitch" class="onoffswitch-checkbox" id="cbid{{offerrowitem.index}}" v-model="offerrowitem.oistate">
				  <label class="onoffswitch-label" for="myonoffswitch"></label>     
				</div>
			  </td>
			  <td>
			  &nbsp;
			  </td>
			  <td>
				<a @click="togglecheck">{{ offerrowitem.hr_title }}</a>
			  </td>
			</tr>
		</table>
	</li>
</template>




<style>


@media only screen and (max-width: 768px) {
  html body div.app ul.list-group li.list-group-item table.row-fluid tbody tr td a {
    font-size: 60px;
    color:orange;
  }
}

ul{line-height:200%;}
p{font-size:120%;line-height:1.2;}
body {font-size:16px}
.onoffswitch {
  position: relative;
  width: 55px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
}

.onoffswitch-checkbox {
  display: none;
}

.onoffswitch-label {
  display: block;
  overflow: hidden;
  cursor: pointer;
  height: 20px;
  padding: 0;
  line-height: 20px;
  border: 0px solid #FFFFFF;
  border-radius: 30px;
  background-color: #9E9E9E;
}

.onoffswitch-label:before {
  content: "";
  display: block;
  width: 30px;
  margin: -5px;
  background: #FFFFFF;
  position: absolute;
  top: 0;
  bottom: 0;
  right: 31px;
  border-radius: 30px;
  box-shadow: 0 6px 12px 0px #757575;
}

.onoffswitch-checkbox:checked + .onoffswitch-label {
  background-color: #42A5F5;
}

.onoffswitch-checkbox:checked + .onoffswitch-label,
.onoffswitch-checkbox:checked + .onoffswitch-label:before {
  border-color: #42A5F5;
}

.onoffswitch-checkbox:checked + .onoffswitch-label .onoffswitch-inner {
  margin-left: 0;
}

.onoffswitch-checkbox:checked + .onoffswitch-label:before {
  right: 0px;
  background-color: #2196F3;
  box-shadow: 3px 6px 18px 0px rgba(0, 0, 0, 0.2);
}

a {
  padding-left: 5px;
}

.disabled {
  color: orange;
}


/* some simple transitions to make the upvote and downvote
buttons fade in as a visual cue for the user */

.glyphicon {
  opacity: 1;
  transition: opacity .25s ease-in-out;
  -moz-transition: opacity .25s ease-in-out;
  -webkit-transition: opacity .25s ease-in-out;
}

.glyphicon:hover {
  opacity: 0.75;
  cursor: pointer;
}

</style>



<script>
export default {
  props: ['offerrowitem','socketemit'],
  methods: {
	togglecheck: function() {

	  this.offerrowitem.oistate = !this.offerrowitem.oistate;

     // lightStatus = '17439298:0:on';
     // socket.emit('lightStatus', lightStatus);

    //console.log(this.offerrowitem.hr_title,this.offerrowitem.index,this.offerrowitem.oistate);
    this.socketemit(this.offerrowitem);
	  }
  }
}
</script>

