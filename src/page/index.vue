<template>
  <div>
    <Theader></Theader>
    <div class="article_list">
      <ul>
        <li v-for="i in list" :key='i.id'>
          <time v-text="$utils.standardTime(i.create_at)"></time>
          <router-link :to="'/content/' + i.id">
          {{i.title}}
          </router-link>
        </li>
      </ul>
    </div>
    <Tfooter></Tfooter>
    <div class="love"></div>
  </div>
</template>

<script>
import Theader from '../components/header.vue'
import Tfooter from '../components/footer.vue'
export default {
  components: {
    'Theader': Theader,
    'Tfooter': Tfooter
  },
  data: function () {
    return {
      list: []
    }
  },
  created () {
    this.getData()
  },
  methods: {
    getData () {
      this.$api.get('topics', null, r => {
        this.list = r.data
      })
    }
  }
}
</script>

<style lang="scss" >
@import "../style/scss/index";
</style>



