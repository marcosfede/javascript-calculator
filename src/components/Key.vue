<template>
<button  @click="clck(value)">
<slot>{{valuetobutton(value)}}</slot>
</button>
</template>

<script>
export default {
  name: 'Key',
  props: ['value', 'clck'],
  methods : {
    clicked : function () {
      this.$emit(this.value)
    },
    valuetobutton : function (value) {
      switch (value) {
        case '*':
          return '×'
        case '/':
          return '÷'
        case 'pm':
          return '±'
        default:
          return value
      }
    }
  }
}

</script>
<style>
button {
  background-color: inherit;
}
button:focus {outline:0;}
</style>
