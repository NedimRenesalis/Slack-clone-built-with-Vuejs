<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <Vonage v-if="!!server.status && server.status === 'ok'" :server="server" />
    <template v-else>
    <HelloWorld msg="Connecting..."/>
    </template>
  </div>
</template>

<script>
import Vonage from '@/components/Vonage.vue'
import ServerService from '@/services/Server'

export default {
  name: 'App',
  components: {
    Vonage,
},
data () {
return {
server: {},
     }
   },
   mounted () {
     this.getServerStatus()
   },
   methods: {
     getServerStatus () {
       ServerService.fetchStatus()
         .then((response) => {
           this.server = response.data
         })
     }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
