<template>
  <div class="max-w-6xl mx-auto">
    <div class="flex flex-col">
      <div class="py-8 text-center">
        <h3 class="text-5xl font-bold text-green-500">Ekoji Running Track</h3>
      </div>
      <div class="flex flex-row items-start justify-between mt-8">
        <div style="width: 64rem;">
          <div
            class="absolute w-4 h-4 ml-16 bg-gray-500 rounded follower3"
          ></div>
          <div
            class="absolute w-4 h-4 ml-10 bg-yellow-500 rounded follower3"
          ></div>
          <div
            class="absolute w-4 h-4 ml-6 bg-blue-500 rounded follower3"
          ></div>
          <div
            class="absolute w-4 h-4 ml-1 bg-green-500 rounded follower1"
          ></div>
          <div
            class="absolute w-4 h-4 -ml-4 bg-red-500 rounded follower2"
          ></div>
          <div
            class="absolute w-4 h-4 -ml-10 bg-purple-500 rounded follower2"
          ></div>
          <div
            class="absolute w-4 h-4 -ml-16 bg-teal-500 rounded follower2"
          ></div>
          <div
            class="absolute w-4 h-4 -ml-20 bg-pink-500 rounded follower2"
          ></div>
          <svg
            width="933"
            height="20475"
            viewBox="0 0 933 20475"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              class="absolute aa"
              stroke="black"
              d="M448 0C448 0 448 148 448 236C448 291.048 431.328 319.5 392.328 365.5C340.025 427.192 302.077 455.93 260.828 525.5C228.188 580.549 211.019 613.583 194.828 675.5C178.844 736.629 167.186 774.398 178.828 836.5C193.371 914.078 229.743 961.726 271.828 1028.5C313.178 1094.11 343.057 1115.61 392.328 1175.5C447.079 1242.05 484.925 1273.68 551.828 1328C625.657 1387.94 687.255 1396.09 753.828 1464C817.179 1528.62 851.363 1572.11 881.328 1657.5C913.739 1749.86 908.931 1810.09 899.328 1907.5C887.743 2025.01 863.149 2091.16 808.828 2196C749.416 2310.67 699.403 2368.64 603.828 2455.5C511.325 2539.57 413.353 2532.45 335.828 2630.5C264.921 2720.18 224.098 2788.77 228.828 2903C233.91 3025.71 346.136 3061.58 376.828 3180.5C396.254 3255.77 433.23 3294.16 446.328 3373C468.281 3505.15 456.176 3580.89 446.328 3713.5C436.651 3843.81 456.787 3917.18 446.328 4047C436.455 4169.55 485.447 4245.96 446.328 4363C383.125 4552.1 111.615 4503.6 59.3287 4696C-21.6332 4993.92 618.328 4946.27 618.328 5255C618.328 5563.73 59.3287 5505.27 59.3287 5814C59.3287 6122.73 485.089 6094.5 618.328 6373C791.166 6734.27 751.921 7020.96 618.328 7398.5C545.05 7605.59 511.927 7752.85 336.828 7885.5C224.442 7970.64 37.6739 7878.54 3.82764 8025C-23.4278 8142.94 155.327 8543 155.327 8543L347.827 9083.5C347.827 9083.5 501.785 9558.56 461.827 9864C417.407 10203.5 64.4557 10311 90.827 10658.5C128.652 11157 702.293 11103.7 752.827 11601C808.211 12146.1 98.272 12007.6 70.3278 12467C37.0624 13013.9 752.827 12964.1 752.827 13512C752.827 14059.9 105.177 13962.3 155.827 14456.5C196.827 14856.5 353.107 14747.5 461.827 15013C544.327 15214.5 446.959 15380.5 448 15616C448.873 15813.5 448 16121 448 16121"
              fill="#FFFFFF"
            />
          </svg>
        </div>
        <div
          style="width: 12rem; position: -webkit-sticky"
          class="sticky top-0 p-4 border border-gray-300 rounded-xl"
        >
          <div>
            <button
              class="px-4 py-2 mb-2 mr-2 text-white bg-green-500 rounded"
              @click="play"
            >
              Play
            </button>
            <button
              class="px-4 py-2 mb-2 mr-2 text-white bg-green-500 rounded"
              @click="pause"
            >
              Pause
            </button>
            <button
              class="px-4 py-2 mb-2 mr-2 text-white bg-red-500 rounded"
              @click="restart"
            >
              Restart
            </button>
            <button
              class="px-4 py-2 mb-2 mr-2 text-white bg-yellow-500 rounded"
              @click="check"
            >
              Check
            </button>
          </div>
          <div>
            <p>duration: {{ duration }}</p>
            <template v-if="started">
              <div v-for="node in nodes" :key="node.id">
                <p>currentTime: {{ Math.round(node.anim.currentTime) }}</p>
                <p>progress: {{ Math.round(node.progress) }}</p>
                <p>complete: {{ Math.round(node.complete) }}</p>
              </div>
            </template>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import anime from "animejs";

export default {
  data() {
    return {
      nodes: [
        { id: 1, anim: null, complete: false, progress: 0 },
        { id: 2, anim: null, complete: false, progress: 0 },
        { id: 3, anim: null, complete: false, progress: 0 }
      ],
      randomNodes: [],
      // duration: 100000,
      duration: 3000,
      started: false
    };
  },
  mounted() {
    const path = anime.path(".aa");

    this.nodes.map(node => {
      node.anim = anime({
        targets: `.follower${node.id}`,
        translateX: path("x"),
        translateY: path("y"),
        rotate: path("angle"),
        easing: "linear",
        duration: this.duration,
        loop: false,
        autoplay: false,
        update: function(anim) {
          node.progress = Math.round(anim.progress);
        },
        complete: function(anim) {
          node.complete = anim.completed;
        }
      });
    });
  },
  methods: {
    async play() {
      this.started = true;
      // this.playAll();
      await this.playAllRandom();
      // setTimeout(() => {
      //   this.pauseAll();
      // }, 1200);
    },
    check() {
      console.log(this.randomUnfinishedNode());
    },
    pause() {
      this.pauseAll();
    },
    restart() {
      this.restartAll();
      this.pauseAll();
    },
    playAll() {
      this.nodes.map(node => node.anim.play());
    },
    pauseAll() {
      this.nodes.map(node => node.anim.pause());
    },
    restartAll() {
      this.nodes.map(node => node.anim.restart());
    },
    async playAllRandom() {
      const randomNode = this.randomUnfinishedNode();
      randomNode.anim.play();
      await setTimeout(() => {
        randomNode.anim.pause();
      }, 100);
    },
    randomUnfinishedNode() {
      const unfinishedNodes = this.nodes.filter(
        node => node.complete === false
      );
      const random = Math.floor(Math.random() * unfinishedNodes.length);
      return unfinishedNodes[random];
    },
    anyUnfinishedNode() {
      const unfinishedNodes = this.nodes.filter(
        node => node.complete === false
      );
      return unfinishedNodes.length > 0;
    }
  }
};
</script>
