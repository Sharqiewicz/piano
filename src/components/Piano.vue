<template>
  <div>
    <div class="keyboard" id="keyboard">
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
import { gsap } from "gsap";

@Component
export default class Piano extends Vue {
  mounted() {
    this.methods.startAnimations();
  }
  methods = {
    startAnimations: function() {
      gsap.fromTo("#keyboard", { y: "+=300" }, { y: "-=300", duration: 1 });
    },

    playNote: function(key: any) {
        console.log(key);
      const noteAudio: HTMLAudioElement = document.getElementById(key.dataset.note);
      noteAudio.currentTime = 0;
      noteAudio.play();
      key.classList.add("active");
      noteAudio.addEventListener("ended", () => {
        key.classList.remove("active");
      });
    },

    mountPiano: function() {
      const WHITE_KEYS = ["z", "x", "c", "v", "b", "n", "m"];
      const BLACK_KEYS = ["s", "d", "g", "h", "j"];

      const keys = document.querySelectorAll(".key");
      const whiteKeys = document.querySelectorAll(".key.white");
      const blackKeys = document.querySelectorAll(".key.black");

      keys.forEach(key => {
        key.addEventListener("click", () => this.playNote(key));
      });

      document.addEventListener("keydown", e => {
        if (e.repeat) return;
        const key = e.key;
        const whiteKeyIndex = WHITE_KEYS.indexOf(key);
        const blackKeyIndex = BLACK_KEYS.indexOf(key);

        if (whiteKeyIndex > -1) this.playNote(whiteKeys[whiteKeyIndex]);
        if (blackKeyIndex > -1) this.playNote(blackKeys[blackKeyIndex]);
      });
    }
  };
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.keyboard {
  display: flex;
}

.key {
  height: 200px;
}

.white {
  width: 100px;
  background-color: white;
  border: 1px solid #333;
}

.white.active {
  background-color: #ccc;
}

.black {
  width: 60px;
  background-color: black;
  margin-left: -30px;
  margin-right: -30px;
  z-index: 2;
}

.black.active {
  background-color: #333;
}
</style>
