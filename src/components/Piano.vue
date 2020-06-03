<template>
  <div id="keyboard">
    Piano
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import { gsap } from 'gsap';

@Component
export default class Piano extends Vue {
  mounted(){
    this.methods.startAnimations();
  }
  methods = {
    startAnimations: function(){
        gsap.fromTo('#keyboard', { y:'+=300'}, { y: '-=300', duration: 1});
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
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