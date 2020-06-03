<template>
  <div>
    <div class="keyboard">
    <div data-note="C" class="key white"></div>
    <div data-note="Db" class="key black"></div>
    <div data-note="D" class="key white"></div>
    <div data-note="Eb" class="key black"></div>
    <div data-note="E" class="key white"></div>
    <div data-note="F" class="key white"></div>
    <div data-note="Gb" class="key black"></div>
    <div data-note="G" class="key white"></div>
    <div data-note="Ab" class="key black"></div>
    <div data-note="A" class="key white"></div>
    <div data-note="Bb" class="key black"></div>
    <div data-note="B" class="key white"></div>
  </div>

  <audio id="C" src="notes/C.mp3"></audio>
  <audio id="Db" src="notes/Db.mp3"></audio>
  <audio id="D" src="notes/D.mp3"></audio>
  <audio id="Eb" src="notes/Eb.mp3"></audio>
  <audio id="E" src="notes/E.mp3"></audio>
  <audio id="F" src="notes/F.mp3"></audio>
  <audio id="Gb" src="notes/Gb.mp3"></audio>
  <audio id="G" src="notes/G.mp3"></audio>
  <audio id="Ab" src="notes/Ab.mp3"></audio>
  <audio id="A" src="notes/A.mp3"></audio>
  <audio id="Bb" src="notes/Bb.mp3"></audio>
  <audio id="B" src="notes/B.mp3"></audio>
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