<!-- 
Page template which contains all the sites html tags.
This will be rendered when the page loads

The template is written in PUG, which is a JS library.
PUG is an easy-to-code template engine used to code HTML in a more readable fashion
-->
<template lang="pug">
  div.wrap
    div.text-wrap
      h2.comment-title Comment the code
      p.comment-subtitle Below is a small self contained component. The component is a select dropdown with a search field to filter for results. Locate the code in the project and comment each line of code to the best of your ability. If you determine a method used is built into Javascript you should still describe the functionality
    div.component-wrapper
      div.select-search
        //Here you make a div, where you bind a custom data attribute which is the variable id (which is a random number)
        div(:data-selectSearch='id').form-group
        //Here you make a label with the label variable as the text
        label {{ label }}
        //Here you make a div with a onClick-event, which runs the method toggle. This will be the select box
        div(@click='toggle').select-label
          //Inside the div, you make a paragraph with a custom data attribute which is the labelID variable.
          //When a user selects a country, where will be returned a object, where the print variable will be set to the text here
          p(:data-label='labelID') {{ selectedObject.print }}
          span.icon-group
            //Here you use a component called PyramidIcon
            PyramidIcon(className='icon xx-small')
        //Here you make a div with a custom data attribute which is the labelID variable
        div(:data-tar='labelID').select-container
          //Here you make a input field which will be used as the search bar. this input field has a keydown-event which will run the function filter, when a user begins to type i the input field
          //The input field also has a custom data attribute which is the lableID variable
          //The input field also has a v-model attached, which changes the value of the variable searchInput to the user typed value
          input(v-on:keyup='filter' placeholder="search" :data-input='labelID'  v-model='searchInput')
          ul
            //Here you loop through each item in the displayedList array, after that each item gets a onclick-event which runs the function choose, where that items data gets passed through.
            //Each item gets a key which is the items value, and it gets a custom data attribute which is the items print value.
            li(@click='choose(item)' v-for='item in displayedList' :key='item.value' :data-tar='item.print')
              p {{ item.print }}
              span(v-if='item.icon')
</template>

<script>
import PyramidIcon from '~/components/pyramid'

export default {
  //Here you declare the components name
  name: 'ComponentPage',
  //Here you declare which components that is importet into this component
  components: {
    PyramidIcon,
  },
  //Here you declare all the variables that will be used in the component
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
  //
  computed: {
    selectedObject() {
      return this.passedValue
    },
  },
  //These functions whatches for a change, and the runs a function
  watch: {
    //So if you change the variable editMode to something else, then this function will run
    editMode() {
      this.setMode()
    },
    //and if the variable passedValue changes then this function will run
    passedValue() {
      this.isPassed(this.passedValue, this.userSelectedObject)
    },
  },
  //When the component mounts, the variable displayedList will be set to the datalist, and the function setHeight and setMode will run.
  mounted() {
    this.displayedList = this.dataList
    this.setHeight()
    this.setMode()
  },
  //Here you declare every function that will be used in the component
  methods: {
    //This function handles if you can use the select field.
    setMode() {
      //Here you declare a variable called tar, which is the element with the custom data-attribute id
      const tar = document.querySelector(`[data-selectSearch='${this.id}']`)
      //If edit mode is false, the select field gets a class readOnly and returns false.
      //If edit mode is ture, the select field looses the class readOnly and returns true.
      if (this.editMode === false) {
        tar.classList.add('readOnly')
        return false
      } else {
        tar.classList.remove('readOnly')
        return true
      }
    },
    //
    isPassed(object1, object2) {
      if (object1.value !== undefined) {
        return object1
      } else {
        return object2
      }
    },
    //When this functions runs, you first selects the div with the custom data attribute data-tar="labelID"
    //Then you change the div's height property using a switch, this switch looks at the length of the datalist array 
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
    //
    emit(value) {
      this.$emit('select-search', value)
    },
    //This function runs when you choose an item on the list.
    //When you choose an country, you pass that country through the function, and then run three functions.
    //First you run emit function, where you pass through the data object
    //The you run the toggle function
    //And then you run the changeLabel function where you pass through the objects print variable.
    choose(e) {
      this.emit(e.value)
      this.toggle()
      this.changeLabel(e.print)
    },
    //When this functions runs, you have passed through a variable from the selected item, which vil be used to set the label value.
    changeLabel(value) {
      document.querySelector(
        `[data-label='${this.labelID}']`
      ).textContent = value
    },
    //When this functions runs, you take the datalist array, and filter it.
    //You see if something in the dataList array includes what the user has typed in the search field, and if there is a mach, then it returnes that data.
    //and then you set the displayedList array to that data array..
    //If there is only one mach between the datalist and the user input, then it will run three functions and set the searchInput value to null/empty.
    //first it emits the selected value, then it changets the label to the objects print data, and then it toggels.
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
    //This function can't run if the editMode is false.
    //This function does so the user can open the selectbox, and it has a default variable with the value false.
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
