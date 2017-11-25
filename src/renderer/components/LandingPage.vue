<template>
<div class="grid vh-100 vw-100 tc">
  <p class="mb2 area-meta _gray f4 fw6 lh-copy">{{ amountCompleted <= 1 ? `${amountCompleted} Pomodoro` : `${amountCompleted} Pomodoros` }} completed</p>
  <h1 class="mt0 mb4 area-time f-headline fw2 lh-title">{{ displayTime }}</h1>
  <div v-if="!isComplete" class="area-actions">
    <button
      type="button"
      class="mr3 f4 fw2 bn br2 ph3 pv2 pointer inline-flex items-center _gray-shadow _gray _bg-white _all-animate"
      :class="activeStyles"
      @click="handlePlay">
      <svg
        v-if="!isActive"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 64 64"
        aria-labelledby="title"
        aria-describedby="desc"
        role="img"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        width="16"
        height="16"
        style="width: 16px; height: 16px;"
        class="mr2">
        <title>Play</title>
        <desc>A solid styled icon from Orion Icon Library.</desc>
        <path data-name="layer1"
        fill="currentColor" d="M6 2l52 30L6 62V2z"></path>
      </svg>
      <svg
        v-else
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 64 64"
        aria-labelledby="title"
        aria-describedby="desc"
        role="img"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        width="16"
        height="16"
        style="width: 16px; height: 16px;"
        class="mr2">
        <title>Pause</title>
        <desc>A solid styled icon from Orion Icon Library.</desc>
        <path data-name="layer1" fill="currentColor" d="M40 4h12v56H40z"></path>
        <path data-name="layer2" fill="currentColor" d="M12 4h12v56H12z"></path>
      </svg>
      <span v-if="!isActive">Start</span>
      <span v-else>Pause</span>
    </button>
    <button
      v-if="!isActive && inProgress"
      type="button"
      class="f4 fw2 bn br2 ph3 pv2 pointer inline-flex items-center _gray-shadow _gray _bg-white"
      @click="handleReset">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 64 64"
        aria-labelledby="title"
        aria-describedby="desc"
        role="img"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        width="16"
        height="16"
        style=""
        class="mr2">
        <title>Rotate Right</title>
        <desc>A solid styled icon from Orion Icon Library.</desc>
        <path data-name="layer1"
        d="M39.777 28.593l12.26 11.273L62 26l-4.63-3.103-3.332 4.11A26.995 26.995 0 0 0 28 6C13.48 6 2 18.488 2 33a25.791 25.791 0 0 0 26 26 26.924 26.924 0 0 0 18.953-7.719l-4.244-4.241A20.967 20.967 0 0 1 28 53 19.786 19.786 0 0 1 8 33c0-11.203 8.788-21 20-21a20.979 20.979 0 0 1 20.126 16.12l-4.288-3.943z"
        fill="currentColor"></path>
      </svg>
      Reset
    </button>
  </div>
  <div v-else class="area-actions">
    <button
      type="button"
      class="f4 fw2 bn br2 ph3 pv2 pointer inline-flex items-center _gray-shadow _black _bg-yellow _yellow-shadow wobble-hor-bottom"
      @click="handleStop">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 64 64"
        aria-labelledby="title"
        aria-describedby="desc"
        role="img"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        width="16"
        height="16"
        style=""
        class="mr2">
        <title>Stop</title>
        <desc>A solid styled icon from Orion Icon Library.</desc>
        <path data-name="layer1"
        fill="currentColor" d="M8 8h48v48H8z"></path>
      </svg>
      Stop
    </button>
  </div>
</div>
</template>

<script>
export default {
  name: 'landing-page',
  props: ['displayTime', 'isActive', 'isComplete', 'amountCompleted', 'inProgress'],
  data() {
    return {};
  },
  computed: {
    activeStyles() {
      return {
        '_bg-blue': this.isActive,
        _white: this.isActive,
        '_blue-shadow': this.isActive,
      };
    },
  },
  methods: {
    toggleActive() {
      this.$emit('toggleActive');
    },
    handlePlay() {
      this.toggleActive();
      if (!this.isActive) {
        this.$emit('startTimer');
      } else {
        this.$emit('stopTimer');
      }
    },
    handleReset() {
      this.$emit('resetButton');
    },
    handleStop() {
      this.$emit('resetTimer');
    },
  },
};
</script>

<style>
.grid {
  display: grid;
  grid-template-areas: "meta" "time" "actions";
  grid-template-columns: 1fr;
  grid-template-rows: repeat(3, auto);
  justify-content: center;
  align-content: center;
}

.area-meta { grid-area: meta; }
.area-time { grid-area: time; }
.area-actions { grid-area: actions; }
</style>
