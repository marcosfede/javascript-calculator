<template>
<div id="app" v-on:keyup="handleClick">
    <div id="calculator">
    <div id="top-bar"></div>
    <div id="screen">
        <span>{{current }}</span>
    </div>
    <div id="cal-body">
        <div class="row" id="first-row">
            <Key :clck="handleClick" class="button" :value="current ? 'C' : 'AC'"></Key>
            <Key :clck="handleClick" class="button" value="pm"></Key>
            <Key :clck="handleClick" class="button" value="%"></Key>
            <Key :clck="handleClick" class="button operator" value="/"></Key>
        </div>
        <div class="row" id="second-row">
            <Key :clck="handleClick" class="button" value="7"></Key>
            <Key :clck="handleClick" class="button" value="8"></Key>
            <Key :clck="handleClick" class="button" value="9"></Key>
            <Key :clck="handleClick" class="button operator" value="*"></Key>
        </div>
        <div class="row" id="third-row">
            <Key :clck="handleClick" class="button" value="4"></Key>
            <Key :clck="handleClick" class="button" value="5"></Key>
            <Key :clck="handleClick" class="button" value="6"></Key>
            <Key :clck="handleClick" class="button operator" value="-"></Key>
        </div>
        <div class="row" id="fourth-row">
            <Key :clck="handleClick" class="button" value="1"></Key>
            <Key :clck="handleClick" class="button" value="2"></Key>
            <Key :clck="handleClick" class="button" value="3"></Key>
            <Key :clck="handleClick" class="button operator" value="+"></Key>
        </div>
        <div class="row" id="fifth-row">
            <Key :clck="handleClick" class="button long" value="0"></Key>
            <Key :clck="handleClick" class="button" value="."></Key>
            <Key :clck="handleClick" class="button operator" value="="></Key>
        </div>
    </div>
  </div>
    <div id="madeby">
      <p> made by <a href="https://github.com/marcosfede">marcosfede</a></p>
    </div>
</div>
</template>

<script>
import Key from './components/Key.vue'
export default {

    name: 'App',

    created: function (){
      window.addEventListener('keyup', this.handleKey)
    },

    components: {
        Key
    },

    data() {
        return {
            block: '',
            current: '0',
            lastkey: null
        }
    },

    watch : {
      current : function (val) {
        if (val.length > 9) { this.current = val.slice(0,9)}
      }
    },

    methods: {
        handleKey : function(key){
          let k = key.key
          switch (k){
              case 'Enter':
              case '=':
                  this.Equal()
                  break
              case 'Backspace':
                  this.Clear('C')
                  break
              // case 'AC':
              //     this.Clear(k)
              //     break
              // case 'pm':
              //     this.inputPM()
              //     break
              case '%':
                  this.inputPercent()
                  break
              case '+':
              case '-':
              case '*':
              case '/':
                  this.inputOperator(k)
                  break
              case '.':
                  this.inputDot()
                  break
              case '1':
              case '2':
              case '3':
              case '4':
              case '5':
              case '6':
              case '7':
              case '8':
              case '9':
              case '0':
                  this.inputDigit(k)
                  break
          }
        },
        handleClick: function(k) {
            switch (k) {
                case '=':
                    this.Equal()
                    break
                case 'C':
                case 'AC':
                    this.Clear(k)
                    break
                case 'pm':
                    this.inputPM()
                    break
                case '%':
                    this.inputPercent()
                    break
                case '+':
                case '-':
                case '*':
                case '/':
                    this.inputOperator(k)
                    break
                case '.':
                    this.inputDot()
                    break
                default:
                    this.inputDigit(k)
            }
        },

        evaluate: function(num) {
            return (+eval(num).toFixed(8)).toString()
        },

        inputOperator: function(operator) {
            if (this.current === '') {
              this.block = this.block.slice(0,-1)+operator
            }
            else {
                this.block += '(' + this.current + ')' + operator
                this.current = ''
            }
            this.lastkey = operator
        },

        inputDigit: function(digit) {
            if (this.lastkey === '=') this.current = ''
            if (digit === '0') {
                if (this.current !== '0') {
                    this.current += digit
                }
            } else if (this.current === '0') {
                this.current = digit
            } else {
                this.current += digit
            }
            this.lastkey = digit
        },

        inputDot: function() {
            if (this.current.indexOf('.') === -1) {
                this.current += '.'
            }
            this.lastkey = '.'
        },

        inputPercent: function() {
            if (this.block === '') {
                this.current = this.evaluate(this.current + '/100')
            } else {
                this.current = this.evaluate(this.block.slice(0, -1) + '*' + this.current + '/100')
            }
            this.lastkey = '%'
        },

        inputPM: function() {
            if (this.current[0] === '-') {
                this.current = this.current.slice(1)
            } else {
                this.current = "-" + this.current
            }
            this.lastkey = 'pm'
        },

        Clear: function(key) {
            if (key === 'C') this.current = '0'
            else if (key === 'AC') this.block = ''
            this.lastkey = key
        },

        Equal: function() {
            this.block += '(' + this.current + ')'
            console.log(this.block)
            this.current = this.evaluate(this.block)
            this.block = ''
            this.lastkey = '='
        },
    }
}
</script>

<style>
body,
html {
    font: 100 14px 'Roboto';
    background-color: #ddd;
}
#calculator {
    width: 320px;
    margin: 80px auto auto auto;
    display: flex;
    flex-direction: column;
    background: black;
    box-shadow: 0px 0px 20px 0px #aaa;
}
#madeby {
  background-color: inherit;
  margin-top: 30px;
  display: flex;
  justify-content: center;
}
#madeby a {
  text-decoration: none;
  font-weight: bold;
}
#screen {
    color: white;
    display: flex;
    justify-content: flex-end;
    align-items: flex-end;
    height: 100px;
    width: 320px;
    background-color: #202020;
}

#screen>span {
    padding-right: 18px;
    padding-bottom: 5px;
    font-size: 4em;
}

#cal-body {
    background-color: #E0E0E0;
}

#first-row {
    background-color: #D6D6D6;
}

.row {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
}

.button {
    width: 80px;
    height: 80px;
    background-color: inherit;
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
    box-shadow: inset 0px 0px 80px 0px rgba(0, 0, 0, 0.25);
}

.button.long {
    width: 160px;
}

.button.operator {
    background-color: #F28310;
    color: white;
}
@media screen
  and (max-device-width: 414px)
  and (-webkit-min-device-pixel-ratio: 2) {
  html,body {
    font: 100 36px 'Roboto';
  }
  #calculator {
    width: 832px;
  }
  #screen {
    width: 832px;
    height: 220px;
  }
  .button {
    width: 208px;
    height: 208px;
  }
  .button.long {
    width: 416px;
  }
  #screen>span {
      padding-right: 50px;
      padding-bottom: 15px;
  }
}
</style>
