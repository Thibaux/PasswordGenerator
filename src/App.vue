<template>
  <div id="app">
    <Generator />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Generator from './components/Generator.vue';

@Component({
  components: {
    Generator,
  },
})
export default class App extends Vue {}
</script>

<style lang="scss">
@import 'assets/styles/main.scss';

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: $font;
  text-align: center;
  display: flex;
  align-content: center;
  justify-content: center;
  width: 100vw;
  height: 100vh;
}
</style>
