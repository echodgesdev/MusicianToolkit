<template>
  <div class="recorder">
    <h2>{{ title }}</h2>
    <body>
      {{ foo }}

      <div class="audio-wrapper">
        <audio src="" controls class="js-audio audio"></audio>
      </div>
    </body>
    <footer>
      <button><i v-on:click="start()" class="fa-solid fa-circle"></i></button>
      <button><i v-on:click="stop" class="fa-solid fa-square"></i></button>
    </footer>
  </div>
</template>

<script>
export default {
  name: "Recorder",
  props: {
    title: String,
  },
  setup() {
    let isRecording = false;
    // We'll save all chunks of audio in this array.
    const chunks = [];

    // We will set this to our MediaRecorder instance later.
    let recorder = null;
    //const bar = reactive({ name: "hi" });

    let audioElement = null;

    return { isRecording, chunks, recorder, audioElement };
  },
  mounted() {
    this.audioElement = document.querySelector(".js-audio"); //is there a more "vue way to do this"

    // We'll get the user's audio input here.
    navigator.mediaDevices
      .getUserMedia({
        audio: true, // We are only interested in the audio
      })
      .then((stream) => {
        // Create a new MediaRecorder instance, and provide the audio-stream.
        this.recorder = new MediaRecorder(stream);

        // Set the recorder's eventhandlers
        this.recorder.ondataavailable = this.saveChunkToRecording;
        this.recorder.onstop = this.saveRecording;
      });
  },
  methods: {
    start: function (event) {
      if (this.isRecording === false) {
        this.isRecording = !this.isRecording;
        this.recorder.start();
      }
    },
    stop: function (event) {
      if (this.isRecording === true) {
        this.isRecording = !this.isRecording;
        this.recorder.stop();
      }
    },
    saveChunkToRecording: function (event) {
      this.chunks.push(event.data);
    },
    saveRecording: function (event) {
      const blob = new Blob(this.chunks, {
        type: "audio/mp4; codecs=opus",
      });
      const url = URL.createObjectURL(blob);

      this.audioElement.setAttribute("src", url);
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