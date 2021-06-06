<template>
  <main>
    <header>
      <h2>Generator 3000</h2>
      <div class="passwordResult">
        {{ password }}sldkfj;sdlkjf;slkdjf;lskdjf
      </div>
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
          <div class="checkboxDiv">
            <input type="checkbox" id="toggle" />
            <label for="toggle" class="toggleWrapper">
              <div class="toggle"></div>
            </label>
          </div>
        </div>
        <div class="setting">
          <p>Include numbers</p>
          <div class="checkboxDiv">
            <input type="checkbox" id="toggle" />
            <label for="toggle" class="toggleWrapper">
              <div class="toggle"></div>
            </label>
          </div>
        </div>
        <div class="setting">
          <p>Include symbols</p>
          <div class="checkboxDiv">
            <input type="checkbox" id="toggle" />
            <label for="toggle" class="toggleWrapper">
              <div class="toggle"></div>
            </label>
          </div>
        </div>
      </div>
    </section>
    <footer>
      <div class="generateButtonDiv">
        <button class="generateButton" @click="generatePassword">
          Generate
        </button>
      </div>
    </footer>
  </main>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

type complexObjectInterface = {
  upper: boolean;
  symbol: boolean;
  number: boolean;
};

@Component
export default class Generator extends Vue {
  private passwordLenght: number = 25;
  private password: string = "";
  private settingsChecked: Array<object> = [
    {
      upper: true,
      symbol: true,
      number: true,
    },
  ];

  private type tplotOptions = {
    [key: string]: boolean
}

  private secureMathRandom() {
    return (
      window.crypto.getRandomValues(new Uint32Array(1))[0] /
      (Math.pow(2, 32) - 1)
    );
  }

  private generateLowerCase() {
    return String.fromCharCode(Math.floor(Math.random() * 26) + 97);
  }

  private generateUpperCase() {
    return String.fromCharCode(Math.floor(Math.random() * 26) + 65);
  }

  private generateSymbol() {
    const symbols = '~!@#$%^&*()_+{}":?><;.,';
    return symbols[Math.floor(Math.random() * symbols.length)];
  }

  private generateNumber() {
    return String.fromCharCode(Math.floor(this.secureMathRandom() * 10) + 48);
  }

  private shuffleCharacters($password: string) {
    let result: string;
    let password = $password;

    password.split("");
    let passwordChars = [...password];
    let n = passwordChars.length;

    for (var i = n - 1; i > 0; i--) {
      var j = Math.floor(Math.random() * (i + 1));
      var tmp = passwordChars[i];
      passwordChars[i] = passwordChars[j];
      passwordChars[j] = tmp;
    }
    result = passwordChars.join("");
    return result;
  }

  private generatePassword() {
    let password: string = "";
    let lenghtOfPassword: number = 0;
    let temp: number = 0;
    let lowerChar: string = "";
    let upperChar: string = "";
    let symbolChar: string = "";
    let numberChar: string = "";
    let key: string = "";

    this.settingsChecked[0][upper];

    // for (key in this.settingsChecked) {
    //   if (this.settingsChecked.hasOwnProperty(key)) {
    //     console.log(this.settingsChecked[]);
    //     console.log(key);
    //     temp++;
    //   }
    // }

    // console.log(temp);

    // lenghtOfPassword = Math.round(this.passwordLenght / divider);

    // console.log(lenghtOfPassword);

    // lenghtOfPassword =
    // this.passwordLenght / this.valuetoseewhichcheckboxesareclicked;

    for (let index = 0; index < lenghtOfPassword; index++) {
      lowerChar = this.generateLowerCase();
      upperChar = this.generateUpperCase();
      symbolChar = this.generateLowerCase();
      numberChar = this.generateUpperCase();

      password += lowerChar += upperChar += symbolChar += numberChar;
    }

    this.password = this.shuffleCharacters(password);

    // console.log(this.password);
    // console.log(this.password.length);
  }
}
</script>

<style scoped lang="scss">
@import "./../assets/styles/main.scss";

main {
  display: flex;
  flex-direction: column;
  align-items: center;
  align-self: center;
  justify-content: space-between;
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
    padding-bottom: 0.8em;
  }

  .passwordResult {
    background-color: $color_orange;
    border-radius: 8px;
    height: auto;
    width: 90%;
    padding: 0.5em;
    margin-left: 5%;
    display: none;
  }
}

section {
  margin-top: 10%;
  height: 50%;
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
      height: 3.5em;
      width: 100%;
      border-radius: 3px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding-left: 1em;
      padding-right: 1em;
      background-color: $color_light_gray;

      &:not(:last-child) {
        margin-bottom: 2em;
      }
    }

    .lenghtSliderDiv {
      width: 100%;
      display: flex;
      align-items: center;
      justify-content: space-between;
      background-color: transparent;

      .lenghtSlider {
        width: 80%;
      }

      p {
        padding-top: 0.6em;
        padding-right: 0.5em;
        font-size: 125%;
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

// Checkbox magic
.checkboxDiv {
  input {
    display: none;
  }

  .toggleWrapper {
    z-index: 3;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: all 0.2s;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background-color: #fe4551;

    &:active {
      width: 35px;
      height: 35px;

      .toggle {
        height: 7px;
        width: 7px;
      }
    }

    .toggle {
      transition: all 0.2s ease-in-out;
      height: 4px;
      width: 4px;
      background-color: transparent;
      border: 10px solid #fff;
      border-radius: 50%;
      cursor: pointer;

      animation: red 0.7s linear forwards;
    }
  }

  .background {
    position: absolute;
    height: 100vh;
    width: 100vw;
    background-color: #fef5f4;
  }

  input:checked {
    & ~ .background {
      background-color: #f9faf7;
    }
    & + .toggleWrapper {
      background-color: #48e98a;

      .toggle {
        width: 0;
        background-color: #fff;
        border-color: transparent;
        border-radius: 30px;
        animation: green 0.7s linear forwards !important;
      }
    }
  }

  @keyframes red {
    0% {
      height: 30px;
      width: 0;
      border-width: 2px;
    }
    55% {
      height: 13px;
      width: 27px;
      border-width: 5px;
    }

    70% {
      height: 20px;
      width: 20px;
      border-width: 5px;
    }

    85% {
      height: 15px;
      width: 25px;
      border-width: 5px;
    }

    100% {
      height: 20px;
      width: 20px;
      border-width: 5px;
    }
  }

  @keyframes green {
    0% {
      height: 10px;
      width: 10px;
      border-width: 3px;
    }
    25%,
    55%,
    85% {
      height: 20px;
      width: 2px;
      border-width: 3px;
    }

    40%,
    70%,
    100% {
      height: 20px;
      width: 0;
      border-width: 3px;
    }
  }
}

// Range slider magic
$color__default: rgba(255, 255, 255, 0.8);
$color__hover: rgba(255, 255, 255, 1);
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
