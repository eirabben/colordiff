<template>
  <div class="app">
    <div class="colors">
      <div v-for="(color, index) in colors" class="color" :style="{ backgroundColor: color.value }">
        <color-input v-model="color.value"></color-input>
        <a class="color-action" href="#" v-if="colors.length > 1" v-on:click.prevent="removeColor(index)">Remove</a>
      </div>
    </div>

    <a class="add-color" href="#" v-on:click.prevent="addColor">
      <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-plus"><line x1="12" y1="5" x2="12" y2="19"></line><line x1="5" y1="12" x2="19" y2="12"></line></svg>
    </a>
  </div>
</template>

<script>
import ColorInput from './ColorInput'

export default {
  name: 'app',
  components: {
    ColorInput
  },

  data () {
    return {
      colors: [
        {
          value: ''
        },
      ]
    }
  },

  methods: {
    addColor: function() {
      console.log('adding color')
      this.colors.push({ value: '' })
    },

    removeColor: function(index) {
      this.colors.splice(index, 1)
    }
  }
}
</script>

<style lang="scss">
@import '~normalize.css';

$breakpoint: 576px;

.app {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen-Sans, Ubuntu, Cantarell, "Helvetica Neue", sans-serif;
  height: 100vh;
  display: grid;
  grid-template-columns: auto;
  grid-template-rows: 1fr 3rem;
  grid-template-areas:
    "main"
    "toolbar";

  @media (min-width: $breakpoint) {
    grid-template-columns: 1fr 3rem;
    grid-template-rows: auto;
    grid-template-areas: "main toolbar";
  }
}

.colors {
  grid-area: main;
  display: flex;
  flex-direction: column;
  overflow-y: auto;

  @media (min-width: $breakpoint) {
    overflow-y: auto;
    flex-direction: row;
    grid-column: 1 / span 2;
    grid-row: 1;
  }
}

.color {
  min-height: 8rem;
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-end;
  padding: 2rem;
}

.color-input {
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  background: none;
  border: none;
  text-align: center;
  font-size: 2rem;
  text-transform: uppercase;
  color: rgba(0, 0, 0, 0.5);
  cursor: pointer;
  transition: color 0.1s ease;
  display: block;
  width: 100%;

  &::placeholder {
    color: rgba(0, 0, 0, 0.1);
  }

  &:hover {
    color: rgba(0, 0, 0, 0.7);
  }

  &:focus {
    outline: none;
    color: rgba(0, 0, 0, 0.7);
    &::placeholder {
      color: rgba(0, 0, 0, 0);
    }
  }

}

.color-action {
  text-decoration: none;
  color: rgba(0, 0, 0, 0.3);
  margin-top: 1rem;
  transition: color 0.1s ease;

  &:hover {
    color: rgba(0, 0, 0, 0.5);
  }
}

.add-color {
  background-color: rgba(0, 0, 0, 0.5);
  grid-area: toolbar;
  color: #fff;
  font-size: 2rem;
  text-decoration: none;
  line-height: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background-color 0.1s ease;

  &:hover {
    background-color: rgba(0, 0, 0, 0.7);
  }

  @media (min-width: $breakpoint) {
    padding: 1rem 0;
    align-self: center;
    background-color: rgba(0, 0, 0, 0.5);
    border-top-left-radius: 3px;
    border-bottom-left-radius: 3px;
  }
}
</style>
