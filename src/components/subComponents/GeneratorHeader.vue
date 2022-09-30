<template>
  <header>
    <h2>Generator 3000</h2>
    <div
      id="resultPassword"
      v-bind:class="{
        showResultPassword: showResult,
      }"
      v-clipboard="() => password"
      @click="copiedPopup()"
    >
      <span
        class="copiedPopup"
        v-bind:class="{
          showCopiedPopup: showCopiedPopup,
        }"
        >Password copied!</span
      >
      {{ password }}
    </div>
  </header>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class GeneratorHeader extends Vue {
  @Prop({ default: 'GeneratorHeader' }) readonly name!: string;
  @Prop({ default: false }) showResult!: boolean;
  @Prop({ default: '' }) password!: string;

  private showCopiedPopup: boolean = false;

  private copiedPopup() {
    this.showCopiedPopup = true;
  }
}
</script>

<style scoped lang="scss">
@import './../../assets/styles/main.scss';

header {
  font-size: 100%;
  height: auto;
  width: 100%;
  padding-top: 2em;

  h2 {
    padding-bottom: 0.8em;
  }

  .showResultPassword {
    background-color: $color_orange;
    border-radius: 8px;
    height: auto;
    width: 90%;
    padding: 1em 0.5em;
    margin-left: 5%;
    word-wrap: break-word;
    cursor: pointer;
  }

  .copiedPopup {
    visibility: hidden;
    width: 9em;
    color: whitesmoke;
    text-align: center;
    border-radius: 3px;
    padding: 0.5rem;
    position: absolute;
    z-index: 1;
    margin-top: 2em;
    margin-left: 8em;
  }

  .showCopiedPopup {
    visibility: visible;
  }
}
</style>
