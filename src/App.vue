<template>
  <div id="app">
      <h1>Image classification using MobileNet</h1>
    <p>The MobileNet model labeled this as
    <span ref="result">...</span> with a confidence of
    <span ref="confidence">...</span></p>
    <img src="pikachu.png" crossorigin="anonymous" width="400" ref="image">
    <img src="pikachu2.png" crossorigin="anonymous" width="400" ref="image2">
    <img src="pikachu3.png" crossorigin="anonymous" width="400" ref="image3">
    <img src="pikachu5.jpg" crossorigin="anonymous" width="400" ref="image9">
    <img src="purasuru1.png" crossorigin="anonymous" width="400" ref="image4">
    <img src="purasuru2.jpg" crossorigin="anonymous" width="400" ref="image5">
    <img src="purasuru3.jpg" crossorigin="anonymous" width="400" ref="image6">
    <img src="purasuru4.jpeg" crossorigin="anonymous" width="400" ref="image8">
    <img src="pikachu4.jpg" crossorigin="anonymous" width="400" ref="image7">
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'app',
  components: {
    HelloWorld
  },

  async mounted () {    
      const featureExtractor = ml5.featureExtractor('MobileNet', () => {
        console.log('Model Loaded!');
      });
      const trainClassifier = featureExtractor.classification();
      await trainClassifier.addImage(this.$refs.image, 'pikachu');
      await trainClassifier.addImage(this.$refs.image2, 'pikachu');
      await trainClassifier.addImage(this.$refs.image3, 'pikachu');
      await trainClassifier.addImage(this.$refs.image9, 'pikachu');
      await trainClassifier.addImage(this.$refs.image4, 'purasuru');
      await trainClassifier.addImage(this.$refs.image5, 'purasuru');
      await trainClassifier.addImage(this.$refs.image6, 'purasuru');
      await trainClassifier.addImage(this.$refs.image8, 'purasuru');

      await trainClassifier.train(function(lossValue) {
        console.log('Loss is', lossValue)
      });

      console.log(this.$refs.image7)

      trainClassifier.classify(this.$refs.image7, function(err, result) {
        console.log(result)
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
