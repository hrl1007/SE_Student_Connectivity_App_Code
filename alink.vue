
<style lang="scss">

.alink{
}

</style>


<template lang="pug">
a.alink(:href="to",target="_blank")
  slot
</template>


<script>
//import XXX from './components/XXX'

export default {
  name: 'alink',
  props:['to'],
  data () {
    return {
      msg: 'this is from alink.vue'
    }
  },
  methods: {

  }
}
</script>
