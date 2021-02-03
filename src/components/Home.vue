<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h1>{{lastvalue}}</h1>
  </div>
</template>

<script>
import io from "socket.io-client";

export default {
  name: 'Home',
  props: {
    msg: String
  },
    mounted() {
    this.socket.on('message', (data) => {
      const enc = new TextDecoder("utf-8");
      this.lastvalue = JSON.parse(enc.decode(data)).value;
    });
  },
  data() {
    return {
      lastvalue: 0,
      socket: io('https://d4e1-iot-server.herokuapp.com/'),
    };
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
