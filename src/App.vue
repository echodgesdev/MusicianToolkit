<template>
  <h1>Musician's Toolkit</h1>
  <!--<RecorderVue title="Recorder" />-->
  <PitchPipe title="Pitch Pipe" />
</template>

<script>
import RecorderVue from "./components/Recorder.vue";
import PitchPipe from "./components/PitchPipe.vue";
export default {
  name: "App",
  components: {
    RecorderVue: RecorderVue,
    PitchPipe: PitchPipe,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
