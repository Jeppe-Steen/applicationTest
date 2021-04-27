<template>
  <svg
    id="Layer_1"
    :class="className"
    data-name="Layer 1"
    xmlns="http://www.w3.org/2000/svg"
    xmlns:xlink="http://www.w3.org/1999/xlink"
    viewBox="0 0 400 320.49"
  >
    <defs>
      <clipPath id="clip-path">
        <rect class="cls-1" x="3.35" y="5.43" width="393.31" height="230.12" />
      </clipPath>
    </defs>
    <g class="cls-2">
      <path
        class="cls-3"
        d="M174.13,223.2c14.29,16.46,37.47,16.46,51.76,0l163-187.95c14.3-16.47,8.22-29.81-13.58-29.81H24.68C2.88,5.44-3.2,18.78,11.05,35.25Z"
      />
    </g>
  </svg>
</template>

<script>
export default {
  name: 'PyramidComponent',
  props: {
    className: {
      type: String,
      default() {
        return !this.props.className ? 'icon small' : this.props.className
      },
    },
  },
}
</script>

<style scoped lang="scss">
$icon-xx-small: 15px;
.icon {
  display: inline-block;
  align-self: center;

  &.xx-small {
    width: $icon-xx-small;
    height: $icon-xx-small;
  }
}
.cls-1 {
  fill: none;
}
.cls-2 {
  clip-path: url(#clip-path);
}
.cls-3 {
  fill: #939598;
}
</style>
