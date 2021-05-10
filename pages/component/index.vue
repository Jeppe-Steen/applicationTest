<template lang="pug">
  div.text-wrap
    h2.title Create a component
    p.subtitle On this page is shown a screenshot of a component, the task is fairly simple. Create a component, that displays some of the data in the data property on this page. For any assets or information that are lacking you are free to interpret as you see fit. For any design that are specified and are within your ability you are expected to recreated it to the best of your ability
    img(src="~/assets/build_component.png").picture
    // Build component below this line.


    div.component
      header.componentHeader
        h3.componentHeading Institutioner
        button.componentButton Opret ny
      div.listContainer
        header.listHeader
          h4.institution Institution
          h4.id id
        ul.list
          //every list item, is made out of a component, which is being mapped from the list array
          //I also pass the data from each object through the component, so it can be used later.
          ListItem(v-for="items in list" :id="items.data[2].value" :title="items.data[1].value" :image="items.data[0].href")
</template>

<script>
import ListItem from '~/components/listItem'

export default {
  name: 'CommentPage',
  components: {
    ListItem,
  },
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

<style scoped lang="scss">
.text-wrap {
  display: flex;
  justify-content: center;
  max-width: 550px;
  margin: 0 auto;
  flex-direction: column;
  text-align: center;
  align-items: center;
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

.picture {
  width: 100%;
}

.component {
  width: 170%;
  height: fit-content;
  background-color: #373a3f;
  margin-top: 10px;
  display: flex;
  flex-direction: column;
  padding: 10px;

  .componentHeader {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    padding: 10px 20px;
    background-color: #303032;

    .componentHeading {
      color: #a5a4a4;
      font-size: 0.7em;
      text-transform: uppercase;
    }

    .componentButton {
      padding: 7px 15px;
      border-radius: 5px;
      border: none;
      color: #fff;
      background: rgb(237, 66, 82);
      background: linear-gradient(
        45deg,
        rgba(237, 66, 82, 1) 0%,
        rgba(238, 93, 66, 1) 100%
      );
    }
  }

  .listContainer {
    margin-top: 20px;

    .listHeader {
      display: grid;
      grid-template: auto / 15% 30% 40% 15%;
      grid-template-areas: ' . institution id . ';
      font-size: 0.7em;
      text-transform: uppercase;
      padding: 5px 0;
      color: #a5a4a4;

      .institution {
        width: 100%;
        grid-area: institution;
        display: flex;
      }

      .id {
        grid-area: id;
        display: flex;
      }
    }

    .list {
      list-style: none;
      display: flex;
      flex-direction: column;
      margin: 0;
      padding: 0;
      gap: 10px;
    }
  }
}
</style>
