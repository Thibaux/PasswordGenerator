<template>
  <footer>
    <div class="generateButtonDiv">
      <button class="generateButton" @click="addPasswordValues">
        Generate
      </button>
    </div>
  </footer>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class GeneratorFooter extends Vue {
  @Prop({ default: 'GeneratorFooter' }) readonly name!: string;
  @Prop() passwordLength!: number;

  private addPasswordValues() {
    let times: number;
    let passwordValues: string = '';
    let password: string = '';

    times =
      Math.floor(
        this.passwordLength / Object.values(this.settingsChecked).length
      ) + 1;

    for (let index = 0; index < times; index++) {
      passwordValues = this.generatePasswordValues();
      password += passwordValues;
    }

    password = this.shuffleCharacters(password);
    this.password = password.slice(0, -1);

    this.showResult = true;
  }
}
</script>

<style scoped lang="scss">
@import './../../assets/styles/main.scss';
</style>
