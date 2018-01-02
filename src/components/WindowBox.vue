<template>
  <div class="window" v-scrollBottom>
    <div class="windowContainer" >
      <ul>
        <li v-for="item in resultList">
          <div class="command">
            <span>&rsaquo;</span>
            {{item.commandText}}
          </div>
          <div class="result" v-html="item.result">

          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'WindowBox',
  data () {
    return {

    }
  },
  props: ['resultList'],
  directives: {
    scrollBottom: {
      componentUpdated: function (el) {
        el.scrollTop = el.scrollHeight
      }
    }
  }
}
</script>

<style>
.window {
  height: 100%;
  box-sizing: border-box;
  background-color: #000;
  font-size: 14px;
  color: #ccc;
  overflow: auto;
  border: 1px solid #000;
  box-shadow: 0 0 5px rgba(0,0,0,0.5);
}
.windowContainer {
  width:100%;
}
.window li {
  display: block;
  width: 100%;
  box-sizing: border-box;
  padding: 5px 0 10px 5px;
}
.command {
  color: green;
}
.command::selection {
  color: #000;
  background-color: green;
}
.result {
  width: 100%;
  word-wrap: break-word;
}
.result::selection {
  color: #000;
  background-color: #fff;
}
</style>
