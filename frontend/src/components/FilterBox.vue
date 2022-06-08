<template>
  <div :class="filterName + ' filter-item'" :style="{ backgroundImage: `url(${tempUrl})` }">
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: "filterbox",
  props: {
    tempUrl: String,
    filterName: String,
  },
};
</script>

<style>
.filter-item {
  width: 100px;
  height: 100px;
  margin: 10px 10px 10px auto;
  padding: 8px;
  display: inline-block;
  color: white;
  background-size: cover;
  background-position: center;
}
</style>
