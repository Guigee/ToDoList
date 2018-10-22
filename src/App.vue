<template>
  <div class="todolist">
    <div class="header-main">
      <h1 class="title">肖雯瑶的小记事本</h1>
      <input v-model="inputvalue" class="header-branch1" @click="showAdd" placeholder="eg：大哥今天要做的事">
      <span @click="addItem" class="header-branch2"></span>
    </div>
    <div class="content-list">
      <ul>
        <listitem v-for="(item,index) in list" :key="index" :content="item" :ind="index" @deleate="removeItem(index)"></listitem>
      </ul>
    </div>
  </div>
</template>

<script>
import listItem from './components/listItem.vue'
//更改
export default {
  data: function () {
    return {
      inputvalue: '',
      list: []
    }
  },
  mounted () {
    /* eslint-disable */
    var listindex = store.get('list')||[]
    if(listindex.length){
      for(var i=0;i<listindex.length;i++){
        this.list.push(listindex[i])
      }
      // this.$options.methods.removeItem(this.index)
    }
    $('.header-branch1').keyup(function(e){
      if(e.keyCode==13){
        $('.header-branch2').click()
      }
    })
  }, 
  methods: {
    addItem () {
      if (!this.inputvalue) {
        return this
      } else {
        this.list.push(this.inputvalue)
        this.inputvalue = ''
        /* eslint-disable */
        store.set('list', this.list)
        $('.header-branch2').hide(1000)
      }
    },
    removeItem (e) {
      this.list.splice(e, 1)
      /* eslint-disable */
      store.set('list', this.list)
    },
    showAdd () {
      $('.header-branch2').show(1000)
    }
  },
  components: {
    'listitem': listItem
  }
}
</script>

<style lang="stylus" scoped>
* {
  padding: 0;
  margin: 0;
}
.todolist
  max-width: 500px
  margin: 0 auto
  padding: 0 10px
  .header-main
    font-size: 0
    .title
      display: block
      font-size: 30px
      padding: 10px 0
      color: #ffffff
    .header-branch1
      width: 70%
      padding: 6px
      border-radius: 6px
      background: #F5F5F5
      outline: none
      font-size: 12px
      height: 20px
      line-height: 20px
      border: 0
      vertical-align: top
      box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.3)
      &:hover,&:focus
        background: #fff
        box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.2)
    .header-branch2
      display: inline-block
      background-image: url(../src/components/add.png)
      width: 32px
      height: 32px
      background-size: 32px 32px
      background-repeat: no-repeat
      margin-left: 12px
      vertical-align: middle
      &:hover
        cursor: pointer
  .content-list
    margin-top: 10px
    ul
      list-style: none
</style>
