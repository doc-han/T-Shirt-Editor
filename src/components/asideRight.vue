<template lang="html">
  <div class="content">

    <div class="input">
      <div class="label">
        Select Category
      </div>
      <select class="input-control">
        <option disabled selected>Choose One</option>
        <option value="">Movie</option>
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
      <input type="text" class="input-control" value="GHS 35" disabled>
    </div>

    <div class="input">
      <div class="label">
        Beginner Profit
      </div>
      <input type="text" class="input-control" value="GHS 5" disabled>
    </div>

    <div class="input">
      <div class="label">
        Total Cost
      </div>
      <input type="text" class="input-control" value="GHS 40" disabled>
    </div>

    <button @click="uploadClick()" type="button" class="upload-btn">UPLOAD DESIGN</button>

  </div>
</template>

<script>
import inputTag from 'vue-input-tag'
import {rightToCanvas} from '../main'

export default {
  components: {
    inputTag,
  },
  data(){
    return{
      inputTagProp: {
        value: [],
        placeholder: 'separate with comma',
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
