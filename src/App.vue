<template>
  <div id="app">
      <h1>Image classification using MobileNet</h1>
    <p>The MobileNet model labeled this as
    <span ref="result">...</span> with a confidence of
    <span ref="confidence">...</span></p>
    <img src="bird.jpg"
     crossorigin="anonymous" width="400" ref="image">
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'app',
  components: {
    HelloWorld
  },

  mounted () {
      const image = this.$refs.image;

      const result = this.$refs.result;

      const confidence = this.$refs.confidence;

      const classifier = ml5.imageClassifier('MobileNet', function() {
        console.log('Model Loaded!');
      });

      classifier.predict(image, function(err, results) {
        result.innerText = results[0].label;
        confidence.innerText = results[0].confidence.toFixed(4);
      });  
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
