<template>
  <div class="container">
    <div class="image" />
    <div class="sidebar">Sidebar</div>
    <Slider />
  </div>
</template>

<script>
import Slider from "./components/Slider";

export default {
  components: {
    Slider,
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
  background: limegreen;
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
