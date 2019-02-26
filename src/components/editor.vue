<template lang="html">
  <div>
    <div class="bar">
      <div>
        <i class="fa fa-trash"></i>
      </div>
      <div>
        <i class="fa fa-image"></i>
      </div>
      <div>
        <i class="fa fa-broom"></i>
      </div>
    </div>
    <div class="canvas_bg">
      <div class="image_bg">
        <img id="shirt_img" src="../assets/crew_front.png" alt="">
        <div id="drawing_area">
          <canvas id="canvas" width="300" height="450"></canvas>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
var customjs = require('vue-customjs');
import {leftToCanvas} from '../main';

export default {
  created: function(){
    // Initialising fabirc.js
    var jsCode01 = `
    var cn = new fabric.Canvas('canvas');
    `;
    customjs.add(jsCode01);
    // Listening for the clicked color
    leftToCanvas.$on('clicked-color', function(color){
      document.getElementById('shirt_img').style.backgroundColor = color;
    });
    // Listening for the clicked artwork
    leftToCanvas.$on('clicked-artwork', function(artwork){
      console.log(artwork);
      fabric.Image.fromURL(artwork, function(img){
        cn.add(img);
        cn.renderAll();
      });

    });
  }
}
</script>

<style lang="scss" scoped>
.canvas_bg {
    display: inline-block;
  }
  .image_bg {
    width: 460px;
    height: 575px;
  }
  .image_bg {
    width: 100%;
    height: 100%;
    position: relative;
  }
  #drawing_area {
    position: absolute;
    left: 110px;
    top: 100px;
    width: 300px;
    height: 450px;
  }
  #drawing_area:hover {
    border: 1px solid #343434;
    cursor: pointer;
  }
  .bar {
    height: 40px;
    width: 100%;
    background-color: #fbfbfb;
    border: 1px solid #e8e8e8;
    margin: 3px auto;
    display: flex;
    flex-direction: row;
  }
  .bar div {
    height: 30px;
    line-height: 30px;
    padding: 0 10px;
    font-weight: bold;
    color: #343434;
    border: 1px solid #e8e8e8;
    border-radius: 5px;
    margin: 5px 2px;
    cursor: pointer;
  }
</style>
