<template>
  <main>
    <header>
      <h2>Generator 3000</h2>
      <div class="passwordResult">{{ password }}</div>
    </header>
    <section>
      <div class="settings">
        <p class="smallText">LENGHT:</p>
        <div class="setting lenghtSliderDiv">
          <input
            type="range"
            min="5"
            max="45"
            value="25"
            class="lenghtSlider"
            v-model="passwordLenght"
          />
          <p>{{ passwordLenght }}</p>
        </div>
        <p class="smallText">SETTINGS:</p>
        <div class="setting">
          <p>Include uppercase</p>
        </div>
        <div class="setting">
          <p>Include numbers</p>
        </div>
        <div class="setting">
          <p>Include symbols</p>
        </div>
      </div>
    </section>
    <footer>
      <div class="generateButtonDiv">
        <button class="generateButton">Generate</button>
      </div>
    </footer>
  </main>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class Generator extends Vue {
  private passwordLenght: number = 25;
}
</script>

<style scoped lang="scss">
@import "./../assets/styles/main.scss";

main {
  display: flex;
  flex-direction: column;
  align-items: center;
  align-self: center;
  justify-content: space-evenly;
  background-color: gray;
  width: 25em;
  height: auto;
  border-radius: 5px;
}

header {
  font-size: 100%;
  height: auto;
  width: 100%;
  padding-top: 2em;

  h2 {
    padding-bottom: 2em;
  }

  .passwordResult {
    background-color: $color_orange;
    border-radius: 10px;
    height: auto;
    width: 90%;
    padding: 0.5em;
    margin-left: 5%;
    display: none;
  }
}

section {
  margin-top: 10%;
  height: 60%;
  width: 90%;
  padding-bottom: 2em;

  .settings {
    width: 95%;
    height: 100%;
    margin-left: 2.5%;

    .smallText {
      font-size: 70%;
      width: 100%;
      margin-bottom: 0.5em;
      margin-left: 1em;
      display: flex;
      justify-content: flex-start;
    }

    .setting {
      height: 3em;
      width: 100%;
      border-radius: 3px;
      display: flex;
      align-items: center;
      justify-content: flex-start;
      padding-left: 1em;
      background-color: $color_light_gray;

      &:not(:last-child) {
        margin-bottom: 2em;
      }
    }

    .lenghtSliderDiv {
      width: 100%;
      display: flex;
      align-items: center;
      justify-content: space-evenly;
      background-color: transparent;

      p {
        padding-top: 0.6em;
        font-size: 125%;
      }

      .lenghtSlider {
        width: 80%;
        margin-left: -5%;
      }
    }
  }
}

footer {
  display: flex;
  flex-direction: column;
  justify-content: center;
  height: 4em;
  width: 100%;
  padding-bottom: 1em;
}

// Range slider magic
$color__default: rgba(255, 255, 255, 0.5);
$color__hover: rgba(255, 255, 255, 0.7);
$color__active: rgba(255, 255, 255, 1);

input[type="range"] {
  box-sizing: border-box;
  font-size: 12px;
  line-height: 1;
  // height: 2em;
  background-color: transparent;
  cursor: pointer;
  -webkit-appearance: none;
  width: 100%;

  &::-webkit-slider-thumb {
    -webkit-appearance: none;
  }

  &:focus {
    outline: none;
  }

  &::-ms-track {
    width: 100%;
    cursor: pointer;
    background: transparent;
    border-color: transparent;
    color: transparent;
  }

  &::-webkit-slider-thumb {
    -webkit-appearance: none;
    width: 2em;
    height: 2em;
    margin-top: 0;
    // background-color: ;
    border-radius: 1em;
    border: 2px solid $color__default;
    cursor: pointer;
  }

  &::-ms-thumb {
    width: 2em;
    height: 2em;
    margin-top: 0;
    // background-color: ;
    border-radius: 1em;
    border: 2px solid $color__default;
    cursor: pointer;
  }

  &:hover {
    &::-webkit-slider-thumb {
      border-color: $color__hover;
    }
    &::-moz-range-thumb {
      border-color: $color__hover;
    }
    &::-ms-thumb {
      border-color: $color__hover;
    }
  }

  //&:focus,
  &:active {
    &::-webkit-slider-thumb {
      border-color: $color__active;
    }
    &::-moz-range-thumb {
      border-color: $color__active;
    }
    &::-ms-thumb {
      border-color: $color__active;
    }
  }

  // * * * TRACK * * *

  &::-webkit-slider-runnable-track {
    width: 100%;
    cursor: pointer;
    height: 1em;
    border-bottom: 2px solid $color__default;
    background-color: transparent;
  }

  &:focus::-webkit-slider-runnable-track {
    width: 100%;
    cursor: pointer;
    height: 1em;
    border-bottom: 2px solid $color__default;
    background-color: transparent;
  }

  &::-moz-range-track {
    width: 100%;
    cursor: pointer;
    height: 1em;
    border-bottom: 2px solid $color__default;
    background-color: transparent;
  }

  &::-ms-track {
    background: transparent;
    border-color: transparent;
    color: transparent;
  }
}
</style>
