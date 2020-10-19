<template>
  <div class="m-8">
    <div>
      <div class="w-4 -m-2 absolute rounded h-4 bg-green-500 follower"></div>
      <svg
        width="200"
        height="200"
        viewBox="0 0 200 200"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          class="aa absolute"
          stroke="#000"
          stroke-width="1"
          d="M0 25C0 11.1929 11.1929 0 25 0H175C188.807 0 200 11.1929 200 25V175C200 188.807 188.807 200 175 200H25C11.1929 200 0 188.807 0 175V25Z"
          fill="#FFFFFF"
        />
      </svg>
    </div>
    <div class="mt-4">
      <button @click="play">Play</button>
      <button @click="pause">Pause</button>
    </div>
  </div>
</template>

<script>
import anime from "animejs";

export default {
  data() {
    return {
      anime: undefined
    };
  },
  mounted() {
    const path = anime.path(".aa");

    this.anime = anime({
      targets: ".follower",
      translateX: path("x"),
      translateY: path("y"),
      rotate: path("angle"),
      easing: "linear",
      duration: 10000,
      loop: true,
      autoplay: false
    });
  },
  methods: {
    play() {
      this.anime.play()
    },
    pause() {
      this.anime.pause()
    }
  },
};
</script>
