<template>
  <div class="recorder">
    <h2>{{ title }}</h2>

    <select @change="onChange($event)">
      <option
        v-for="instrument in defaultInstruments"
        :key="instrument"
        :value="instrument.name"
      >
        {{ instrument.name }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  name: "PitchPipe",
  props: {
    title: String,
  },
  setup() {
    const defaultInstruments = [
      {
        name: "Guitar (Standard)",
        notes: ["E2", "A2", "D3", "G3", "B3", "E3"],
      },
      {
        name: "Ukulele (Standard)",
        notes: ["G4", "C4", "E4", "A4"],
      },
      {
        name: "Major Triad",
        notes: ["C4", "E4", "G5"],
      },
    ];

    let selectedInstrument = null;

    return { defaultInstruments, selectedInstrument };
  },
  mounted() {},
  methods: {
    start: function (event) {},
    onChange: function (event) {
      console.log(event.target.value);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>