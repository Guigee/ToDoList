<template>
  <div class="list-item">
    <li class="content">{{content}}</li>
    <span @click="remove" class="remove"></span>
    <span class="finish" @click="finished" :class="{'current': favo}"></span>
  </div>
</template>

<script>
export default {
  props: ['content', 'ind'],
  data: function () {
    return {
      favo: false,
      favoo: []
    }
  },
  created () {
    /* eslint-disable */
    var median = store.has('favoo') ? store.get('favoo') : []
  },
  methods: {
    remove () {
      this.$emit('deleate', this.ind)
    },
    finished () {
      this.favo = !this.favo
      /* eslint-disable */
      store.set('favoo', this.favo)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" scoped>
  .list-item
    margin: 5px 0
    font-size: 0
    .content
      display: inline-block
      width: 70%
      padding: 4px
      background: #eeeeee
      border-radius: 6px
      box-shadow: 2px 2px 1px #ffffff
      vertical-align: middle
      font-size: 12px
    .remove
      display: inline-block
      background-image: url(remove-circle-outline.png)
      width: 25px
      height: 25px
      background-size: 25px 25px
      background-repeat: no-repeat
      margin-left: 5px
      vertical-align: middle
    .finish
      display: inline-block
      background-image: url(finish.png)
      width: 25px
      height: 25px
      background-size: 25px 25px
      background-repeat: no-repeat
      margin-left: 5px
      vertical-align: middle
      &.current
        background-image: url(finished.png)
</style>
