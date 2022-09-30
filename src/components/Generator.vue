<template>
  <main>
    <GeneratorHeader
      :showResult="showResult"
      :password="password"
    ></GeneratorHeader>
    <section>
      <div class="settings">
        <p class="smallText">LENGTH</p>
        <div class="setting lengthSliderDiv">
          <input
            type="range"
            min="5"
            max="45"
            value="25"
            class="lengthSlider"
            v-model="passwordLength"
          />
          <p>{{ passwordLength }}</p>
        </div>
        <p class="smallText">SETTINGS</p>
        <div class="setting">
          <p>Include uppercase</p>
          <div class="settingCheckbox">
            <input
              checked
              @click="addCheckedSettingToArray('generateUpperCase')"
              type="checkbox"
              id="toggle"
            />
          </div>
        </div>
        <div class="setting">
          <p>Include numbers</p>
          <div class="settingCheckbox">
            <input
              checked
              type="checkbox"
              id="toggle"
              @click="addCheckedSettingToArray('generateNumber')"
            />
          </div>
        </div>
        <div class="setting">
          <p>Include symbols</p>
          <div class="settingCheckbox">
            <input
              checked
              @click="addCheckedSettingToArray('generateSymbol')"
              type="checkbox"
              id="toggle"
            />
          </div>
        </div>
      </div>
    </section>
  </main>
  <GeneratorFooter :passwordLength="passwordLength"></GeneratorFooter>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import { GeneratorHeader } from '@/components/subComponents';
import GeneratorFooter from '@/components/subComponents/GeneratorFooter.vue';

@Component({
  components: {
    GeneratorFooter,
    GeneratorHeader,
  },
})
export default class Generator extends Vue {
  private showResult: boolean = false;
  private passwordLength: number = 25;
  private password: string = '';
  public settingsChecked: string[] = [
    'generateLowerCase',
    'generateUpperCase',
    'generateSymbol',
    'generateNumber',
  ];

  private addCheckedSettingToArray($setting: string) {
    if (!this.settingsChecked.includes($setting)) {
      this.settingsChecked.push($setting);
    } else if (this.settingsChecked.includes($setting)) {
      const index = this.settingsChecked.indexOf($setting);

      if (index > -1) {
        this.settingsChecked.splice(index, 1);
      }
    }
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

    password.split('');
    let passwordChars = [...password];
    let n = passwordChars.length;

    for (let i = n - 1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i + 1));
      const tmp = passwordChars[i];
      passwordChars[i] = passwordChars[j];
      passwordChars[j] = tmp;
    }
    result = passwordChars.join('');
    return result;
  }

  private generatePasswordValues() {
    let password: string = '';
    let settingValue: string = '';

    Object.values(this.settingsChecked).forEach((element) => {
      switch (element) {
        case 'generateLowerCase':
          settingValue = this.generateLowerCase();
          break;
        case 'generateUpperCase':
          settingValue = this.generateUpperCase();
          break;
        case 'generateSymbol':
          settingValue = this.generateSymbol();
          break;
        case 'generateNumber':
          settingValue = this.generateNumber();
          break;
      }

      password += settingValue;
    });

    return password;
  }
}
</script>

<style scoped lang="scss">
@import './../assets/styles/main.scss';

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
      color: white;
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
      background: url('./../assets/img/cool-background-setting-div.png')
        no-repeat center fixed;
      background-size: cover;

      &:not(:last-child) {
        margin-bottom: 2em;
      }
    }

    .lengthSliderDiv {
      width: 100%;
      display: flex;
      align-items: center;
      justify-content: space-between;
      background-color: transparent;

      .lengthSlider {
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

  .generateButtonDiv button {
    display: inline-block;
    padding: 0.35em 1.2em;
    border: 0.1em solid #ffffff;
    margin: 0 0.3em 0.3em 0;
    border-radius: 0.12em;
    text-decoration: none;
    box-sizing: border-box;
    font-weight: 500;
    font-size: 1.2em;
    text-align: center;
    transition: all 0.2s;
    color: whitesmoke;
    background-image: url('./../assets/img/cool-background-button-div.png');
    background-size: cover;
  }

  .generateButtonDiv button:hover {
    cursor: pointer;
    opacity: 0.5;
  }

  @media all and (max-width: 30em) {
    .generateButtonDiv button {
      display: block;
      margin: 0.4em auto;
    }
  }
}

// Range slider magic
$color__default: rgba(0, 0, 0, 0.8);
$color__hover: rgba(0, 0, 0, 1);
$color__active: rgba(0, 0, 0, 1);

input[type='range'] {
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
