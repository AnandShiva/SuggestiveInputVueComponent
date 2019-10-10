<template>
  <div id="app">
    <SuggestiveInput :suggestionProps="suggestionInp"/>
    <br>
    
    <SuggestiveInput :suggestionProps="suggestionInp" />

  </div>
</template>

<script>
import SuggestiveInput from './components/SuggestiveInput.vue';

export default {
  name: 'app',
  components: {
    SuggestiveInput
  }, 
  data(){
    return {
      suggestionInp : [
         "Products",
        "Electronics",
        "Unnecessaryly loooonnggggg textttttttttttttt",
        "short text",
        "Special Characters & ",	
        "12345678910111213",
        "Television",
        "VueJS",
        "Component Sharing", 
				"Zebra-Crossing"
      ]
    };
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
