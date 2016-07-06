<template>
  <div class="app">
  
   
  <ul class="list-group">
    <component-a v-for="item in dataitems" :offerrowitem="item" :socketemit="onSocketEmit"></component-a>
  </ul>
  </div>

</template>

<script>
import ComponentA from './ComponentA.vue'
import ComponentB from './ComponentB.vue'

export default {
  components: {
    ComponentA,
    ComponentB
  },
  ready: function() {
   
    //  var lightStatus = '17439298:0:on';
    //  socket.emit('lightStatus', lightStatus);
    /*$.get('/items.json', function(items) {
        this.items = items;
    }.bind(this), 'json');*/
  },
  data () {

     var socket = io.connect('http://192.168.1.145:8000')
     // Set listeners
     socket.on('notification', this.onSocketNotification);
     //
    return {
      socket: socket,
      dataitems: [{"hr_title":"staandelamp","oistate":false,"index":"0"},
{"hr_title":"wc","oistate":false,"index":"1"},
{"hr_title":"trappehuis boven","oistate":false,"index":"2"},
{"hr_title":"tv","oistate":false,"index":"3"},
{"hr_title":"slaapkamer","oistate":false,"index":"4"},
{"hr_title":"radio","oistate":false,"index":"5"},
{"hr_title":"lampkachel","oistate":false,"index":"6"}]
    }
  },
methods: {
    onSocketNotification: function (data) {
      console.log('<onSocketNotification:',data);
      var bfdata = '{"hr_title":"wc","oistate":"1","usb":"1"}';
      bfdata = JSON.parse(data);
      console.warn(bfdata['hr_title']);
      console.warn(bfdata['oistate']);
      var fnditem = this.dataitems.find(x=> x.hr_title == bfdata['hr_title']);
      console.warn(fnditem.oistate);
      if (bfdata['oistate'] == 1)
        fnditem.oistate=true
        else
         fnditem.oistate=false;
      console.info(fnditem);
    }
    ,
    onSocketEmit: function (data) {
    //console.log('>onSocketEmit:');
    //  var lightStatus = '17439298:0:on';
    
    //console.log(data);
    //var btnstate = (data.iostate) ? 'on' : 'off';
    var cmd= '{"hr_title":\"'+data.hr_title+"\",\"new_state\":"+data.oistate+"}";
    //{"hr_title":"lampkachel","new_state":"0","index":"6"}
    console.log('>onSocketEmit cmd:',cmd);
    this.socket.emit('lightStatus', cmd);
    }
  }

}



</script>
