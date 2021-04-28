<template lang="pug">
  div.text-wrap
    h2.title Create a component
    p.subtitle On this page is shown a screenshot of a component, the task is fairly simple. Create a component, that displays some of the data in the data property on this page. For any assets or information that are lacking you are free to interpret as you see fit. For any design that are specified and are within your ability you are expected to recreated it to the best of your ability
    img(src="~/assets/build_component.png")
    // Build component below this line.
</template>

<script>
export default {
  name: 'CommentPage',
  data() {
    return {
      list: [
        {
          id: '5fc43c695061fa2544a0e1f8',
          data: [
            { isImage: true, href: 'http://placeimg.com/640/480/city' },
            { value: 'Refined Concrete Pizza' },
            { value: '2-1-4-DK-88715-F26E2E' },
          ],
        },
        {
          id: '5fc43c695061fa2544a0e1fa',
          data: [
            { isImage: true, href: 'http://placeimg.com/640/480/city' },
            { value: 'Rustic Wooden Chips' },
            { value: '2-5-3-1-4-DK-57583-0008-727EE1' },
          ],
        },
        {
          id: '5fc43c695061fa2544a0e1fc',
          data: [
            { isImage: true, href: 'http://placeimg.com/640/480/city' },
            { value: 'Handmade Fresh Car' },
            { value: '1-5-3-4-DK-28664-60BE3E' },
          ],
        },
        {
          id: '5fc43c695061fa2544a0e1fe',
          data: [
            { isImage: true, href: 'http://placeimg.com/640/480/city' },
            { value: 'Tasty Rubber Computer' },
            { value: '1-4-DK-64880-0026-B2D166' },
          ],
        },
        {
          id: '5fc43c695061fa2544a0e200',
          data: [
            { isImage: true, href: 'http://placeimg.com/640/480/city' },
            { value: 'Incredible Plastic Cheese' },
            { value: '4-2-DK-58418-3860-34CF64' },
          ],
        },
      ],
    }
  },
}
</script>

<style scoped>
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
