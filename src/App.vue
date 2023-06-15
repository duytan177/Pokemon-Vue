<template>
  <main-screen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeStart($event)"
  ></main-screen>
  <interac-screen
    v-if="statusMatch === 'match'"
    :cardsContext="setting.cardsContext"
    @onFinish="onGetResult"
  ></interac-screen>
  <result-screen
    v-if="statusMatch === 'result'"
    :timer="timer"
    @onStartAgain="statusMatch = 'default'"
  ></result-screen>
  <copy-right-screen></copy-right-screen>
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteracScreen from "./components/InteractScreen.vue";
import { shuffled } from "./utils/array";
import ResultScreen from "./components/ResultScreen.vue";
import CopyRightScreen from "./components/CopyRightScreen.vue";

export default {
  name: "App",
  components: {
    MainScreen,
    InteracScreen,
    ResultScreen,
    CopyRightScreen,
  },
  data() {
    return {
      setting: {
        totalBlocks: 0,
        cardsContext: [],
        startedAt: null,
      },
      statusMatch: "default",
      timer: 0,
    };
  },
  methods: {
    onHandleBeforeStart(config) {
      console.log("runnign handdle before start", config);
      this.setting.totalBlocks = config.totalBlocks;
      const firstCards = Array.from(
        { length: this.setting.totalBlocks / 2 },
        (_, i) => i + 1
      );

      const secondCards = [...firstCards];
      const cards = [...firstCards, ...secondCards];
      console.log(cards);
      this.setting.cardsContext = shuffled(shuffled(shuffled(shuffled(cards))));
      console.log(cards);
      this.setting.startedAt = new Date().getTime();
      this.statusMatch = "match";
    },

    onGetResult() {
      //get timer
      this.timer = new Date().getTime() - this.setting.startedAt;

      //switch tyo result component
      this.statusMatch = "result";
    },
  },
};
</script>
<style lang="css" scoped>
.copyright {
  position: fixed;
  left: 50%;
  transform: translateX(-50%);
  bottom: 1.5rem;
  color: var(--light);
  z-index: 3;
  font-size: 1.5rem;
}

.copyright a {
  color: #f4dc26;
}
</style>
