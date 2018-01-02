<template>
  <input type="text" class="inputBox" spellcheck="false" v-model="command" v-focus
  @keydown.enter="start"
  @keydown.up="perCommand"
  @keydown.down="nextCommand" />
</template>

<script type="text/javascript">
  export default {
    name: 'inputBox',
    data () {
      return {
        command: '',
        currentCommandId: -1
      }
    },
    props: ['commandList', 'focus'],
    directives: {
      focus: {
        inserted: function (el) {
          el.focus()
        }
      }
    },
    watch: {
      focus: function () {
        this.$el.focus()
      }
    },
    methods: {
      start () {
        var command = this.command.trim()
        this.commandList.push(command)
        this.$emit('runCommand', command)
        this.command = ''
        this.currentCommandId = -1
      },
      setCommandId (id) {
        if (id !== -1) {
          this.command = this.commandList[id]
        } else {
          this.command = ''
        }
        this.currentCommandId = id
      },
      perCommand () {
        var id = this.currentCommandId - 1
        if (id === -1) { id = 0 }
        if (id < -1) { id = this.commandList.length - 1 }
        this.setCommandId(id)
      },
      nextCommand () {
        if (this.currentCommandId === -1) {
          return false
        }
        var id = this.currentCommandId + 1
        if (id >= this.commandList.length) { id = -1 }
        this.setCommandId(id)
      }
    }
  }
</script>

<style scoped>

input{
  position: absolute;
  left: 0;
  bottom: -30px;
  height: 30px;
  width: 100%;
  box-sizing: border-box;
  background-color: #222;
  border: 1px solid #000;
  color: #fff;
  text-indent: 5px;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.5);
  outline: none;
}

</style>
