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

    <button type="button" class="btn_artwork" name="button"> <i class="fa fa-upload"></i> Upload artwork</button>

    <div class="input">
      <div class="label">
        Artworks
      </div>
      <div class="artworks">
        <img class="artworks-item" src="https://vuejs.org/images/logo.png" alt="">
        <img class="artworks-item" src="https://vuejs.org/images/logo.png" alt="">
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

  .btn_artwork {
    width: calc(100% - 20px);
    padding: 5px 0;
    font-size: 20px;
    border: 1px solid #e8e8e8;
    border-radius: 5px;
    margin-top: 10px;
    cursor: pointer;
  }
  .artworks {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
  }
  .artworks-item {
    height: 100px;
    width: 130px;
    margin-bottom: 10px;
  }


</style>
