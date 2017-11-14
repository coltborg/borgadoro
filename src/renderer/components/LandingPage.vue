<template>
<div class="grid">
  <p>{{ count }} Pomodoro Today</p>
  <h1>25:00</h1>
  <div>
    <button>Start</button>
    <button>Reset</button>
  </div>

</div>
</template>

<script>
export default {
  name: 'landing-page',
  data() {
    return {
      count: 0,
    };
  },
  methods: {
    open(link) {
      this.$electron.shell.openExternal(link);
    },
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Nunito:300,400,600');

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Nunito', sans-serif;
}


</style>
