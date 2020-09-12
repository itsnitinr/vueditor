<template>
  <div class="container">
    <div class="image" :style="imageStyles" />
    <div class="sidebar">
      <SidebarItem
        v-for="(option, index) in options"
        :key="option.property"
        :option="option"
        :index="index"
        :active="selectedOptionIndex === index"
        @handleClick="selectOption"
      />
    </div>
    <Slider :min="getMin" :max="getMax" :value="getValue" @sliderChange="handleSliderChange" />
  </div>
</template>

<script>
import Slider from "./components/Slider";
import SidebarItem from "./components/SidebarItem";
import DEFAULT_OPTIONS from "./default";

export default {
  components: {
    Slider,
    SidebarItem,
  },
  data() {
    return {
      options: DEFAULT_OPTIONS,
      selectedOptionIndex: 0,
      imageStyles: {},
    };
  },
  methods: {
    selectOption(index) {
      this.selectedOptionIndex = index;
    },
    handleSliderChange(value) {
      this.selectedOption.value = value;
      this.getImageStyles();
    },
    getImageStyles() {
      const filters = this.options.map((option) => {
        return `${option.property}(${option.value}${option.unit})`;
      });
      this.imageStyles = { filter: filters.join(" ") };
    },
  },
  computed: {
    selectedOption() {
      return this.options[this.selectedOptionIndex];
    },
    getMin() {
      return this.selectedOption.range.min;
    },
    getMax() {
      return this.selectedOption.range.max;
    },
    getValue() {
      return this.selectedOption.value;
    },
  },
};
</script>

<style>
*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.container {
  display: grid;
  grid-template-columns: 1fr auto;
  grid-template-rows: 1fr auto;
  grid-template-areas:
    "image sidebar"
    "slider sidebar";
  height: 100vh;
  width: 100vw;
  background: #dadada;
}

.image {
  grid-area: image;
  background: url(https://images.unsplash.com/photo-1599863853745-237150e3c879?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=334&q=80);
  height: 100%;
  width: 100%;
  background-repeat: no-repeat;
  background-position: center;
}

.sidebar {
  grid-area: sidebar;
  background: #1d2d50;
  display: flex;
  flex-direction: column;
  align-items: stretch;
}

.sidebar-item {
  cursor: pointer;
  border: none;
  outline: none;
  background: #1d2d50;
  color: white;
  padding: 1rem;
  position: relative;
  transition: background-color 0.2s;
}

.sidebar-item:hover,
.sidebar-item:focus {
  background: #43658b;
}

.sidebar-item.active {
  background-color: #515070;
}

.sidebar-item::after {
  content: "";
  position: absolute;
  width: 100%;
  left: 0;
  bottom: 0;
  height: 1px;
  background: white;
}

.sidebar-item:last-child::after {
  display: none;
}

.slider-container {
  grid-area: slider;
  padding: 2rem;
  margin-top: 2rem;
}

.slider {
  width: 100%;
  cursor: pointer;
}
</style>
