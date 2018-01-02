<template>
  <div class="bar">
    <span>{{title}}</span>
  </div>
</template>

<script>

export default {
  name: 'ToolBar',
  data () {
    return {

    }
  },
  props: ['title']
}
</script>

<style>
.bar{
  height: 30px;
  width: 100%;
  box-sizing: border-box;
  position: absolute;
  left: 0;
  top: -30px;
  background-color: #fff;
  border: 1px solid #444;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.5);
  border-bottom: none;
}
.bar span{
  height: 30px;
  line-height: 30px;
  margin-left: 5px;
  color: #444;
  font-weight: bold;
  float: left;
}
</style>
