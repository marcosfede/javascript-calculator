<template>
  <div id="app">
    <div id="top-bar"></div>
    <div id="screen">
      <span>{{current}}</span>
    </div>
    <div id="cal-body">
      <div class="row" id="first-row">
      <Key :clck="clck" class="button" value="c"></Key>
      <Key :clck="clck" class="button" value="±"></Key>
      <Key :clck="clck" class="button" value="%"></Key>
      <Key :clck="clck" class="button operator" value="÷"></Key>
    </div>
    <div class="row" id="second-row">
      <Key :clck="clck" class="button" value="7"></Key>
      <Key :clck="clck" class="button" value="8"></Key>
      <Key :clck="clck" class="button" value="9"></Key>
      <Key :clck="clck" class="button operator" value="×"></Key>
    </div>
    <div class="row" id="third-row">
      <Key :clck="clck" class="button" value="4"></Key>
      <Key :clck="clck" class="button" value="5"></Key>
      <Key :clck="clck" class="button" value="6"></Key>
      <Key :clck="clck" class="button operator" value="-"></Key>
    </div>
    <div class="row" id="fourth-row">
      <Key :clck="clck" class="button" value="1"></Key>
      <Key :clck="clck" class="button" value="2"></Key>
      <Key :clck="clck" class="button" value="3"></Key>
      <Key :clck="clck" class="button operator" value="+"></Key>
    </div>
    <div class="row" id="fifth-row">
      <Key :clck="clck" class="button long" value="0"></Key>
      <Key :clck="clck" class="button" value="."></Key>
      <Key :clck="clck" class="button operator" value="="></Key>
    </div>
    </div>
  </div>
</template>

<script>
import Key from './components/Key.vue'
export default {

  name: 'App',

  components: {
    Key
  },

  data () {
    return {
      block: '',
      current: ''
    }
  },

  methods: {
      clck : function (k) {
        console.log(k)
        switch (k) {
          case '=':
            this.current = this.block = this.block + this.current
            break
          case 'c':
            this.current = this.block = ''
            break
          case '±':
            this.current = "-"+this.current
            break
          case '%':
            this.block += k
            this.current = ''
            break
          case '+':
            this.block += k
            this.current = ''
            break
          case '-':
            this.block += k
            this.current = ''
            break
          case '×':
            this.block += k
            this.current = ''
            break
          case '÷':
            this.block += k
            this.current = ''
            break
          default:
            this.current += k
        }
    }
  }
}

</script>

<style>
body, html {
  height: 100%;
  font: 100 14px 'Roboto';
  background-color: #ddd;
}
#app {
  width: 320px;
  margin: 100px auto auto auto;
  display: flex;
  flex-direction: column;
  background: black;
  box-shadow: 0px 0px 20px 0px #aaa;
}
#screen {
  color: white;
  display: flex;
  justify-content: flex-end;
  align-items: flex-end;
}
#screen>span {
  font-size: 4em;
}
div.row {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}
.button {
  width: 80px;
  height: 80px;
  background-color: #D2D3D5;
  font: 100 250% 'Roboto';
  border: none;
  padding: 0;
  font-family: inherit;
  display: flex;
  align-items: center;
  justify-content: center;
  border-top: 1px solid #777;
  border-right: 1px solid #777;
}
.button:active {
  box-shadow: inset 0px 0px 80px 0px rgba(0,0,0,0.25);
}
.button.long {
  width: 160px;
}
#screen {
  height: 120px;
  width: 320px;
  background-color: #202020
}
#first-row {
  background-color: #C7C8CA;
}
.button.operator {
  background-color: #F28310;
  color: white;
}
</style>
