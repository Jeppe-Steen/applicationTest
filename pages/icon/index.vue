<template lang="pug">
  div.text-wrap
    h2.title Icon animation
    p.subtitle Below is one or more videos of icons in animation, the task is to replicate the animation as close to resemblance as the videos depicts. Each icon is shown in the code as raw svg code, and can be manipulated as you wish
    div.icon-pair
      div.icon
        svg(class="className"
        data-name="Layer 1"
        xmlns="http://www.w3.org/2000/svg"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        viewBox="0 0 400 400")
          defs
            clipPath(id="clip-path_notificationBell")
              rect(class="cls-1"
              x="49.93"
              y="12.04"
              width="300.13"
              height="375.91")
          g(class="cls-2")
            path(class="cls-3"
            d="M200.29,340.87c12.79,0,25.59.13,38.38-.08,3.48-.06,4.42.83,4,4.81-2.49,22.74-18.85,40.78-38.63,42.23-22.19,1.63-40.66-13.08-45.76-36.46C156,340.9,156,340.9,165.43,340.9h34.86Z")
            path(class="cls-3"
            d="M95.57,281.9c5.51-9.08,10.52-17.87,14.38-27.41,8.25-20.36,12.16-41.81,14.09-63.86,1-12.13.33-24.32,1.45-36.44,3-32.76,27.8-62.83,57.33-69.7,22.6-5.25,43.43-1,61.91,14.17,18.11,14.83,28,35,29.84,59.78,1.17,15.67.76,31.43,2.95,47.06,3.79,27.1,11.11,52.59,26.12,74.91a11.79,11.79,0,0,1,.61,1.49Zm247.86-4.67c-16.4-17.62-27-38.64-32-63.21-3.78-18.71-3.74-37.78-4.76-56.76-1.38-25.88-9.74-48.73-25.26-68.27a105.58,105.58,0,0,0-56.73-37.41c-2.68-.72-3.56-1.92-3.41-4.9.25-4.28.05-8.58-.05-12.88-.25-10.91-9.33-22.71-22.74-21.7-10.83.83-19.64,10.49-19.78,22.81-.05,4-.19,8,0,12,.16,2.82-.7,4-3.23,4.6a94.22,94.22,0,0,0-25.91,10.6C113.25,84.24,94,118,92.82,163.67c-.35,13.32-.6,26.61-2.57,39.77-3.17,21.16-9.3,41-21.42,58.24-4.09,5.8-8.81,10.93-13.22,16.4-6.23,7.72-7.17,16.47-3.62,25.55,3.81,9.69,11.19,13.87,20.69,13.87q63.48,0,127,0v0q32.52,0,65,0c20.77,0,41.53,0,62.3,0,5.82,0,11.16-1.46,15.59-5.71a24.72,24.72,0,0,0,.87-34.6")
      video(controls autoplay="true" loop)
        source(src="~/assets/bellToll.mp4" type="video/mp4")
</template>

<script>
export default {
  name: 'IconPage',
}
</script>

<style scoped>
.icon-pair {
  display: flex;
  justify-content: center;
  max-width: 800px;
  height: auto;
  flex-direction: row;
}

.icon {
  height: 400px;
  width: 400px;
}

.icon svg {
  width: 380px;
  height: 380px;
}

video {
  height: 400px;
  width: 400px;
}

.text-wrap {
  display: flex;
  justify-content: center;
  max-width: 550px;
  margin: 0 auto;
  flex-direction: column;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 60px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 15px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}
</style>
