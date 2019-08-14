<template>
  <div id="app">
    <video  id="player" ref="videoPlayer" autoplay width="1000"></video>
  </div>
</template>

<script>
export default {
  name: 'App',
  mounted () {
    var vm = this
    if (!('mediaDevices' in navigator)) {
      navigator.mediaDevices = {}
    }
    if (!('getUserMedia' in navigator.mediaDevices)) {
      navigator.mediaDevices.getUserMedia = function (constraints) {
        var getUserMedia = navigator.webkitGetUserMedia || navigator.mozGetUserMedia

        if (!getUserMedia) {
          return Promise.reject(new Error('getUserMedia is not implemented!'))
        }

        return new Promise(function (resolve, reject) {
          getUserMedia.call(navigator, constraints, resolve, reject)
        })
      }
    }
    navigator.mediaDevices.getUserMedia({video: true})
      .then(function (stream) {
        vm.$refs.videoPlayer.srcObject = stream
      })
  },
  methods: {
  },
  destroy () {
    var vm = this
    vm.$refs.imagePickerArea.style.display = 'none'
    vm.$refs.videoPlayer.style.display = 'none'
    vm.$refs.canvasElement.style.display = 'none'
  }
}

</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
