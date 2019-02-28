<template lang="html">
  <div>
    <div class="bar">
      <template v-if="toolbar.showActions">
        <div @click="toolbarAction('delete')">
          <i class="fa fa-trash"></i>
        </div>
        <div @click="toolbarAction('clear')">
          <i class="fa fa-broom"></i>
        </div>
      </template>
    </div>
    <div class="canvas_bg">
      <div class="image_bg">
        <img v-if="showFront" id="shirt_img" src="../assets/crew_front.png" alt="">
        <img v-else id="shirt_img" src="../assets/crew_back.png" alt="">
        <div id="drawing_area">
          <canvas id="canvas" width="300" height="450"></canvas>
        </div>
        <div @click="swapShirt()" class="switch_btn">
          <i class="fa fa-exchange-alt"></i>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import {leftToCanvas} from '../main';

// Initialising fabric js // when component is created
var cn = null;

export default {
  data(){
    return {
      toolbar: {
        showActions: true,
      },
      showFront: true
    }
  },
  methods: {
    swapShirt: function(){
      this.showFront = !this.showFront;
    },
    toolbarAction: function(action){
      switch (action) {
        case 'delete':
        try {
            var ob = cn.getActiveObject();
            if(ob != null) cn.remove(ob);
        } catch (e) {
          console.log(e);
        }
          break;
        case 'clear':
          if(confirm("Are you sure you want to clear Everything!!!")){
            //Delete everything drawn on the canvas
          }
        default:

      }

    }
  },
  created: function(){
    // Listening for the clicked color
    leftToCanvas.$on('clicked-color', function(color){
      document.getElementById('shirt_img').style.backgroundColor = color;
    });
    // Listening for the clicked artwork
    leftToCanvas.$on('clicked-artwork', function(artwork){
      // Initialising canvas on first attempt to add object
      if(cn == null){
        cn = new fabric.Canvas('canvas');
        var target = null;
        cn.on('mouse:down',function(options){
          target = options.target;
        });
      }
      fabric.Image.fromURL(artwork, function(img){
        cn.add(img);
        cn.renderAll();
      });

    });
  },
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
  .switch_btn {
    position: absolute;
    top: 10px;
    right: 20px;
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
  .bar div, .switch_btn {
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
  .switch_btn {
    background-color: #343434;
    color: #f9f9f9;
  }
</style>
