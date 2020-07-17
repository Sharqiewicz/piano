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

    <audio id="C"></audio>
    <audio id="Db"></audio>
    <audio id="D"></audio>
    <audio id="Eb"></audio>
    <audio id="E"></audio>
    <audio id="F"></audio>
    <audio id="Gb"></audio>
    <audio id="G"></audio>
    <audio id="Ab"></audio>
    <audio id="A"></audio>
    <audio id="Bb"></audio>
    <audio id="B"></audio>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import { gsap } from "gsap";

@Component
export default class Piano extends Vue {
  mounted() {
    this.methods.startAnimations();
    this.methods.mountPiano();
  }
  methods = {
    startAnimations: function() {
      gsap.set("#keyboard", {autoAlpha: 0 })
      gsap.fromTo("#keyboard", { y: "+=300" }, { y: "-=300", duration: 1, delay: 1, autoAlpha: 1 });
    },

    playNote: function(key: HTMLDivElement) {
      if (key.dataset.note) {
        const noteAudio: HTMLAudioElement | null = document.querySelector(
          `#${key.dataset.note}`
        );
        if (noteAudio instanceof HTMLAudioElement) {
          noteAudio.currentTime = 0;
          noteAudio.play();
          key.classList.add("active");
          noteAudio.addEventListener("ended", () => {
            key.classList.remove("active");
          });
        }
      }
    },

    mountPiano: function() {
      const WHITE_KEYS = ["z", "x", "c", "v", "b", "n", "m"];
      const BLACK_KEYS = ["s", "d", "g", "h", "j"];

      const keys: NodeListOf<HTMLDivElement> = document.querySelectorAll(
        ".key"
      );
      const whiteKeys: NodeListOf<HTMLDivElement> = document.querySelectorAll(
        ".key.white"
      );
      const blackKeys: NodeListOf<HTMLDivElement> = document.querySelectorAll(
        ".key.black"
      );
      const audios: NodeListOf<HTMLAudioElement> = document.querySelectorAll(
        "audio"
      );

      audios.forEach(key => {
        key.src = `${require(`../notes/${key.id}.mp3`)}`;
      });

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
  justify-content: center;
  margin: 50px;
}

.key {
  height: 300px;
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
  height: 200px;
  background-color: black;
  margin-left: -30px;
  margin-right: -30px;
  z-index: 2;
}

.black.active {
  background-color: #333;
}

@media(max-width: 600px){
    .key{
        height: 200px;
        width: 100px;
    }
    .black{
        height: 50px;
    }
}
</style>
