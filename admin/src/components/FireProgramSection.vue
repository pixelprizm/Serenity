<template>
  <form v-on:submit.prevent="onSubmit" class="big-bugs-page-section fire-program-section">
    <h2>or</h2>
    <p>Select a fire program</p>
    <select class="custom-select" name="patternName" id="fireProgramName" v-model="selectedFireProgram">
      <option v-for="programName in fireProgramNames" v-bind:value="programName">{{programName}}</option>
    </select>
    <button class="btn btn-primary">Start Fire Show</button>
  </form>
</template>

<script>
import { getFireProgramNameList, runFireProgram } from '../requests';

export default {
    name: 'FireProgramSection',
    data() {
      return {
        fireProgramNames: [],
        selectedFireProgram: null
      };
    },
    beforeMount() {
      getFireProgramNameList()
        .then(list => {
          this.fireProgramNames = list;
        }, error => {
          console.log(error);
        });
    },
    methods: {
        onSubmit: function() {
          runFireProgram(this.selectedFireProgram)
            .then(() => {
              console.log(`Started fire program ${this.selectedFireProgram}`);
            }, error => {
              console.log(error);
            });
        }
    }
};
</script>

<style>
.fire-program-section button {
  margin-top: 10px;
}
</style>

