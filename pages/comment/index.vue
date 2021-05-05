<!-- 
Page template which contains all the sites html tags.
This will be rendered when the page loads

The template is written in PUG, which is a JS library.
PUG is an easy-to-code template engine used to code HTML in a more readable fashion
-->
<template lang="pug">
  //div container that wraps all the other html tags. The container has the class "wrap"
  div.wrap
    //div container which wraps a h2 tag with the class "comment-title" and a p tag with the class "comment-subtitle"
    div.text-wrap
      h2.comment-title Comment the code
      p.comment-subtitle Below is a small self contained component. The component is a select dropdown with a search field to filter for results. Locate the code in the project and comment each line of code to the best of your ability. If you determine a method used is built into Javascript you should still describe the functionality
    div.component-wrapper
      div.select-search
        div(:data-selectSearch='id').form-group
        label {{ label }}
        div(@click='toggle').select-label
          p(:data-label='labelID') {{ selectedObject.print }}
          span.icon-group
            PyramidIcon(className='icon xx-small')
        div(:data-tar='labelID').select-container
          input(v-on:keyup='filter' placeholder="search" :data-input='labelID'  v-model='searchInput')
          ul
            li(@click='choose(item)' v-for='item in displayedList' :key='item.value' :data-tar='item.print')
              p {{ item.print }}
              span(v-if='item.icon')
</template>

<script>
import PyramidIcon from '~/components/pyramid'

export default {
  name: 'ComponentPage',
  components: {
    PyramidIcon,
  },
  data() {
    return {
      passedValue: {
        type: Object,
        default: () => {
          return {}
        },
      },
      editMode: true,
      label: 'Land',
      searchLabel: 'Land2',
      labelID: '22222',
      dataList: [
        { print: 'Danmark', value: 'denmark' },
        { print: 'Norge', value: 'norway' },
        { print: 'Sverige', value: 'sweden' },
        { print: 'Tyskland', value: 'germany' },
        { print: 'England', value: 'england' },
      ],
      displayedList: [],
      searchInput: '',
      selectedIcon: '',
      userSelectedObject: {},
      id: Math.random(),
    }
  },
  computed: {
    selectedObject() {
      return this.passedValue
    },
  },
  watch: {
    editMode() {
      this.setMode()
    },
    passedValue() {
      this.isPassed(this.passedValue, this.userSelectedObject)
    },
  },
  mounted() {
    this.displayedList = this.dataList
    this.setHeight()
    this.setMode()
  },
  methods: {
    setMode() {
      const tar = document.querySelector(`[data-selectSearch='${this.id}']`)
      if (this.editMode === false) {
        tar.classList.add('readOnly')
        return false
      } else {
        tar.classList.remove('readOnly')
        return true
      }
    },
    isPassed(object1, object2) {
      if (object1.value !== undefined) {
        return object1
      } else {
        return object2
      }
    },
    setHeight() {
      const tar = document.querySelector(`[data-tar='${this.labelID}']`)
      switch (this.dataList.length) {
        case 6:
          tar.style.setProperty('height', '190px')
          break
        case 5:
          tar.style.setProperty('height', '170px')
          break
        case 4:
          tar.style.setProperty('height', '150px')
          break
        case 3:
          tar.style.setProperty('height', '130px')
          break
        case 2:
        case 1:
          tar.style.setProperty('height', '100x')
          break
        default:
          tar.style.setProperty('height', '230px')
          break
      }
    },
    emit(value) {
      this.$emit('select-search', value)
    },
    choose(e) {
      this.emit(e.value)
      this.toggle()
      this.changeLabel(e.print)
    },
    changeLabel(value) {
      document.querySelector(
        `[data-label='${this.labelID}']`
      ).textContent = value
    },
    filter() {
      this.displayedList = [
        // eslint-disable-next-line array-callback-return
        ...this.dataList.filter((e) => {
          if (e.print.toLowerCase().includes(this.searchInput.toLowerCase())) {
            return e
          }
        }),
      ]

      if (this.displayedList.length === 1) {
        this.emit(this.displayedList[0].value)
        this.changeLabel(this.displayedList[0].print)
        this.searchInput = ''
        this.toggle(true)
      }
    },
    toggle(flag = false) {
      if (this.editMode === false) {
        return
      }

      const tar = document.querySelector(`[data-tar='${this.labelID}']`)

      if (flag === true) {
        tar.classList.remove('active')
        return
      }

      if (!tar.classList.contains('active')) {
        this.displayedList = this.dataList
        tar.classList.add('active')
        document.querySelector(`[data-input='${this.labelID}']`).focus()
      } else {
        tar.classList.remove('active')
      }
    },
  },
}
</script>

<style lang="scss">
$color-dark-3: #2a2b2d;
$color-text-light: #ffffff;
$border-radius-medium: 6px;
$shadow-small-inset: inset 0 1px 5px 0px rgba(30, 30, 30, 0.8);
$font-weight-light: 300;
$color-dark-3: #2a2b2d;
$color-dark-2: #242425;
$color-dark-7: #2f3032;

.wrap {
  display: flex;
  justify-content: center;
  flex-direction: column;
  max-width: 800px;
  margin: 0 auto;
}

.text-wrap {
  display: flex;
  justify-content: center;
  max-width: 550px;
  margin: 0 auto;
  flex-direction: column;
  text-align: center;
}

.comment-title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 60px;
  color: #35495e;
  letter-spacing: 1px;
}

.comment-subtitle {
  font-weight: 300;
  font-size: 15px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.component-wrapper {
  margin: 0 auto;
  padding: 40px;
  border-radius: $border-radius-medium;
  background: $color-dark-2;
  width: 400px;
  height: 200px;
}

.icon-group {
  display: inline-flex;
  justify-content: center;
}

.select-search {
  position: relative;
  width: 250px;
  display: flex;
  flex-direction: column;
  padding-left: 15px;
  padding-right: 15px;
  margin-bottom: 20px;
  align-items: center;

  label {
    color: #ffffff;
    margin-bottom: 5px;
    text-transform: uppercase;
    width: 100%;
  }

  .select-label {
    position: relative;
    width: 100%;
    // height: 51px;
    background: $color-dark-3;
    padding: 17px 20px;
    color: $color-text-light;
    border-radius: $border-radius-medium;
    box-shadow: $shadow-small-inset;
    font-weight: $font-weight-light;
    letter-spacing: 0;

    .icon-group {
      position: absolute;
      right: 10px;
      top: 50%;
      transform: translateY(-50%);
    }
  }

  .select-container {
    display: none;
    position: absolute;
    flex-direction: column;
    border: 1px solid $color-dark-2;
    background: $color-dark-3;
    top: 100%;
    left: 15px;
    width: calc(100% - 30px);
    height: 230px;
    z-index: 100;
    overflow: hidden;
    font-weight: $font-weight-light;

    input {
      width: 100%;
      padding: 10px 5px;
      resize: none;
      width: 100%;
      color: #ffffff;
      background-color: #2a2b2d;
      padding: 16px 20px;
      position: relative;
      border-radius: 6px;
      box-shadow: inset 2px 2px 2px 0px rgb(30 30 30 / 80%);
      border: none;

      &::placeholder {
        font-size: 1.2em;
        color: $color-text-light;
      }
    }

    ul {
      transition: cubic-bezier(0.175, 0.885, 0.32, 1.275) 100ms;
      padding: 5px 10px;
      width: calc(100% + 20px);
      max-height: 230px;
      overflow-y: scroll;

      li {
        display: flex;
        flex-direction: row;
        cursor: pointer;
        border-bottom: 1px solid $color-dark-2;
        margin-bottom: 4px;

        p {
          width: 80%;
          color: $color-text-light;
        }

        span {
          width: 20%;
        }

        &.collapse {
          animation: collapse;
          animation-duration: 100ms;
          animation-fill-mode: forwards;
          animation-iteration-count: 1;
          animation-timing-function: cubic-bezier(0.455, 0.03, 0.515, 0.955);
        }
      }
    }

    &.active {
      display: flex;
    }
  }

  &.readOnly {
    .select-label {
      background: $color-dark-7;
      padding: 0px 0px;
      font-size: 14px;

      .icon-group {
        display: none;
      }
    }
  }
}
</style>
