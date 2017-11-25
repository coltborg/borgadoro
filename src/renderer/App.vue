<template>
  <div id="app" class="_black _bg-white">
    <router-view
      :display-time="displayTime"
      :is-active="isActive"
      :is-complete="isComplete"
      :in-progress="inProgress"
      :amount-completed="amountCompleted"
      @startTimer="handleStart"
      @resetButton="handleReset"
      @stopTimer="handleStop"
      @toggleActive="toggleActive"
      @resetTimer="resetTimer"></router-view>
  </div>
</template>

<script>
export default {
  name: 'borgadoro',
  data() {
    return {
      countdownInterval: 0,
      secondsLeft: 0,
      timeToTrack: (25 * 60),
      displayTime: '',
      inProgress: false,
      isActive: false,
      isComplete: false,
      amountCompleted: 0,
    };
  },
  mounted() {
    this.displayTimeLeft(this.timeToTrack);
  },
  methods: {
    handleStart() {
      if (this.secondsLeft <= 0) {
        // TODO: Uncomment when done testing
        // this.timer(this.timeToTrack);
        this.timer(2);
      } else {
        this.timer(this.secondsLeft);
      }
    },
    handleReset() {
      this.clear(this.countdownInterval);
      this.toggleProgress();
      this.displayTimeLeft(this.timeToTrack);
      this.secondsLeft = 0;
    },
    handleStop() {
      this.clear(this.countdownInterval);
    },
    toggleActive() {
      this.isActive = !this.isActive;
    },
    toggleProgress() {
      this.inProgress = !this.inProgress;
    },
    toggleComplete() {
      this.isComplete = !this.isComplete;
    },
    addToCompleted() {
      this.amountCompleted += 1;
    },
    reset() {
      this.displayTimeLeft();
    },
    clear(interval) {
      clearInterval(interval);
    },
    timer(seconds) {
      const now = Date.now();
      const then = now + (seconds * 1000);

      this.clear(this.countdownInterval);

      this.displayTimeLeft(seconds);

      if (!this.inProgress) {
        this.toggleProgress();
      }

      this.countdownInterval = setInterval(() => {
        this.secondsLeft = Math.round((then - Date.now()) / 1000);

        if (this.secondsLeft === 0) {
          this.displayTimeLeft(this.secondsLeft);
          this.finishTimer();
          return;
        }

        this.displayTimeLeft(this.secondsLeft);
      }, 1000);
    },
    resetTimer() {
      this.clear(this.countdownInterval);
      this.toggleComplete();
      this.displayTimeLeft(this.timeToTrack);
      this.secondsLeft = 0;
    },
    finishTimer() {
      this.clear(this.countdownInterval);
      this.toggleActive();
      this.toggleProgress();
      this.toggleComplete();
      this.addToCompleted();
    },
    displayTimeLeft(seconds) {
      const minutes = Math.floor(seconds / 60);
      const remainderSeconds = seconds % 60;
      const display = `${minutes}:${remainderSeconds < 10 ? '0' : ''}${remainderSeconds}`;

      this.displayTime = display;
    },
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Nunito:300,400,600');
@import url('https://unpkg.com/tachyons@4.9.0/css/tachyons.min.css');

:root {
  --black: #253137;
  --gray: #8f9698;
  --white: #ffffff;
  --blue: #0088ff;
  --purple: #7349ff;
  --yellow: #ffc524;
  --peach: #ffc4A8;
}

@keyframes wobble-hor-bottom {
  0%,
  20% {
    transform: translateX(0%);
    transform-origin: 50% 50%;
  }
  3% {
    transform: translateX(-30px) rotate(-6deg);
  }
  6% {
    transform: translateX(15px) rotate(6deg);
  }
  9% {
    transform: translateX(-15px) rotate(-3.6deg);
  }
  12% {
    transform: translateX(9px) rotate(2.4deg);
  }
  15% {
    transform: translateX(-6px) rotate(-1.2deg);
  }
}

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  /* TODO: Remove this soon */
  outline: none;
}

body {
  font-family: 'Nunito', sans-serif;
  font-size: 100%;
}

#app {
  width: 100vw;
  height: 100vh;
}

.vw-100 { width: 100vw; }

._black { color: var(--black); }
._gray  { color: var(--gray); }
._white { color: var(--white); }
._blue  { color: var(--blue); }

._bg-black  { background-color: var(--black); }
._bg-white  { background-color: var(--white); }
._bg-gray   { background-color: var(--gray); }
._bg-blue   { background-color: var(--blue); }
._bg-purple { background-color: var(--purple); }
._bg-yellow { background-color: var(--yellow); }
._bg-peach  { background-color: var(--peach); }

._hover-bg-black:hover  { background-color: var(--black); }
._hover-bg-white:hover  { background-color: var(--white); }
._hover-bg-gray:hover   { background-color: var(--gray); }
._hover-bg-blue:hover   { background-color: var(--blue); }
._hover-bg-purple:hover { background-color: var(--purple); }
._hover-bg-yellow:hover { background-color: var(--yellow); }
._hover-bg-peach:hover  { background-color: var(--peach); }

._bg-animate { transition: background-color 150ms ease-out; }
._color-animate { transition: color 150ms ease-out; }
._all-animate { transition: all 150ms ease-out; }
/* transition: all 150ms cubic-bezier(0.25, 0.8, 0.25, 1); */

._gray-shadow { box-shadow: 0 0.25rem 1rem 0.25rem rgba(143, 150, 152, 0.25); }
._blue-shadow { box-shadow: 0 0.25rem 1rem 0.25rem rgba(0, 136, 255, 0.25); }
._yellow-shadow { box-shadow: 0 0.25rem 1rem 0.25rem rgba(255, 197, 36, 0.25); }

.wobble-hor-bottom { animation: wobble-hor-bottom 3s infinite both; }

.fade-enter-active {
  transition: all 300ms ease-out;
}
.fade-leave-active {
  transition: all 300ms ease-out;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
