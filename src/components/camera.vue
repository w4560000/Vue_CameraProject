<template>
    <video id="video" width="640" height="480" autoplay></video>
</template>

<script>
export default {
  name: 'camera',
  data () {
    return {
      width: 400,
      height: 300,
      src: '',
      autoplay: true,
      mirror: true,
      screenshotFormat: 'image/jpeg'
    }
  }
}
</script>
