<template lang="html">
  <div class="content">

    <h3>TeeSwerg</h3>

    <div class="input">
      <div class="label">
        Design Title
      </div>
      <input type="text" class="input-control">
    </div>

    <div class="input">
      <div class="label">
        Select colors
      </div>
      <div class="colors">
        <div class="color-item" v-for='(color) in config.colors' :style="'background-color: '+color"></div>
      </div>
    </div>

  </div>
</template>

<script>
export default {
  props: ['config']
}
</script>

<style lang="scss" scoped>
$color-item-size: 30px;
  .colors {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
  }
  .color-item {
    width: $color-item-size;
    height: $color-item-size;
    border-radius: 50%;
    margin-right: 10px;
    margin-bottom: 10px;
    cursor: pointer;
  }

</style>
