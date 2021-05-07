<template lang="pug">
    li.listItem
        img(:src="image").listPicture
        h4.listInstitution {{title}}
        p.listId {{ id }}
        span.listOptions
            div.options
              img(src="~/assets/pen.svg")
            div.options
              img(src="~/assets/chard.svg")
            div.options
              img(src="~/assets/bin.svg")
</template>

<script>
export default {
  name: 'ListItem',
  // Here I declare each prop, that is passed through the component. Which i can use later
  props: {
    id: {
      type: String,
      default: '',
    },
    title: {
      type: String,
      default: '',
    },
    image: {
      type: String,
      default: '',
    },
  },
  data() {
    return {}
  },
}
</script>

<style scoped lang="scss">
.listItem {
  display: grid;
  grid-template: 8vh / 15% 30% 40% 15%;
  grid-template-areas: ' listPicture listInstitution listId listOptions';
  font-size: 0.7em;
  width: 100%;
  background-color: #303032;
  color: #a5a4a4;
  align-items: center;
  padding: 5px;

  .listPicture {
    background-color: rgba(144, 238, 144, 0.048);
    height: 50px;
    width: 50px;
    border-radius: 50%;
    margin: auto;
  }

  .listInstitution {
    display: flex;
    grid-area: listInstitution;
  }

  .listId {
    display: flex;
    grid-area: listId;
  }

  .listOptions {
    display: flex;
    flex-direction: row;

    .options {
      height: 30px;
      width: 30px;
      border-radius: 50%;
      background: rgb(237, 66, 82);
      background: linear-gradient(
        45deg,
        rgba(237, 66, 82, 1) 0%,
        rgba(238, 93, 66, 1) 100%
      );
      margin: 2px;
      display: flex;
      align-items: center;
      justify-content: center;

      img {
        height: 40%;
      }
    }
  }
}
</style>
