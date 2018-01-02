<template>
  <div id="app" @click="click">
    <ToolBar :title="title"/>
    <WindowBox :resultList="resultList" />
    <InputBox @runCommand="runCommand" :commandList.sync="commandList" :focus="focus" />
  </div>
</template>

<script>
import ToolBar from './components/ToolBar'
import WindowBox from './components/WindowBox'
import InputBox from './components/InputBox'

export default {
  name: 'app',
  components: {
    ToolBar,
    WindowBox,
    InputBox
  },
  data () {
    return {
      title: 'Terminal',
      // 结果数组
      resultList: [],
      // 历史命令数组
      commandList: [],
      focus: 0,
      // 命令方法映射
      commandMethods: {
        clear () {
          this.resultList = []
          return 'clear done'
        },
        history () {
          var result = ''
          for (var i = 0; i < this.commandList.length; i++) {
            result += '<div>' + i + ': ' + this.commandList[i] + '</div>'
          }
          return result
        }
      }
    }
  },
  created: function () {
    if (!localStorage.getItem('commandList')) {
      localStorage.setItem('commandList', JSON.stringify([]))
    }
    this.commandList = JSON.parse(localStorage.getItem('commandList'))
  },
  methods: {
    // 运行命令
    runCommand (command) {
      var result
      if (this.commandMethods[command]) {
        result = this.commandMethods[command].call(this)
      } else {
        // result = command + ': command is undefined!'
        try {
          result = (function (command) {
            var Fn = Function
            return new Fn('return ' + command)()
          })(command)
        } catch (e) {
          // console.log(e)
          result = command + ': command is undefined!'
        }
      }
      this.resultList.push({
        commandText: command,
        result: result
      })
      localStorage.setItem('commandList', JSON.stringify(this.commandList))
    },
    click () {
      this.focus++
    }

  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
html {
  height: 100%;
}
body {
  height: 100%;
}
#app {
  height: 50%;
  width: 50%;
  box-shadow: 0 0 5px rgba(0,0,0,0.5);
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  margin: auto;

}
</style>
