<template>
  <div>
    <Theader></Theader>
    <h2 v-text="dat.title"></h2>
    <p>作者：{{dat.author.loginname}}  发表于：{{$utils.standardTime(dat.create_at)}}</p>
    <hr>
    <article v-html="dat.content"></article>
    <h3>网友回复: </h3>
    <ul>
      <li v-for="i in dat.replies" :key = 'i.id'>
        <p>评论者: {{i.author.loginname}}  评论于: {{$utils.standardTime(i.create_at)}}</p>
        <article v-html="i.content"></article>
      </li>
    </ul>
    <Tfooter></Tfooter>
  </div>
</template>

<script>
import Theader from '../components/header.vue'
import Tfooter from '../components/footer.vue'

export default {
  components: {
    Theader,
    Tfooter
  },
  data () {
    return {
      id: this.$route.params.id,
      dat: {}
    }
  },
  created () {
    var vm = this
    this.$nextTick(function () {
      vm.getData()
      console.log(this.$route)
    })
  },
  methods: {
    getData () {
      this.$api.get('topic/' + this.id, null, r => {
        this.dat = r.data
      })
    }
  }
}
</script>
