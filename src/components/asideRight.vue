<template lang="html">
  <div class="content">

    <div class="input">
      <div class="label">
        Select Category
      </div>
      <select v-model="config.selectedCategory" class="input-control">
        <option disabled selected>Choose One</option>
        <option v-for="cat in config.categories" :value="cat">{{ cat }}</option>
      </select>
    </div>

    <div class="input">
      <div class="label">
        Keywords
      </div>
    <inputTag v-bind="inputTagProp" class="inputTag"></inputTag>
    </div>

    <div class="input">
      <div class="label">
        Base Cost
      </div>
      <input type="text" class="input-control" :value="'GHS '+config.base" disabled>
    </div>

    <div class="input">
      <div class="label">
        Beginner Profit
      </div>
      <select v-model="config.selectedProfit" class="input-control">
        <option disabled selected>Choose One</option>
        <option v-for="p in config.profit" :value="p">{{ 'GHS '+ p }}</option>
      </select>
    </div>

    <div class="input">
      <div class="label">
        Total Cost
      </div>
      <input type="text" class="input-control" :value="'GHS '+ (parseInt(config.selectedProfit) + parseInt(config.base))" disabled>
    </div>

    <button @click="uploadClick()" type="button" class="upload-btn">UPLOAD DESIGN</button>

  </div>
</template>

<script>
import inputTag from 'vue-input-tag'
import {rightToCanvas} from '../main'

export default {
  props: ['config'],
  components: {
    inputTag,
  },
  data(){
    return{
      inputTagProp: {
        value: [],
        placeholder: 'Press Enter after Keyword',
        readOnly: false,
        addTagOnBlur: false,
        limit: -1,
        validate: 'text',
        addTagOnKeys: [13,188],
        allowDuplicates: false,
        beforeAdding: null
      }
    }
  },
  methods: {
    uploadClick: function(){
      rightToCanvas.$emit('upload-click', '');
    }
  }
}
</script>

<style lang="scss" scoped>
  .upload-btn {
    padding: 10px 15px;
    font-size: 18px;
    background-color: #343434;
    color: #f9f9f9;
    margin-top: 10px;
    border-radius: 5px;
    cursor: pointer;
  }
</style>
