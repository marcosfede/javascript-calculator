<template>
<button @click="clck(value)">
<slot>{{value}}</slot>
</button>
</template>

<script>
export default {

  name: 'Key',
  props: ['value', 'clck'],
  data () {
    return {
    }
  },
  methods : {
    clicked : function () {
      this.$emit(this.value)
    }
  }
}

</script>
