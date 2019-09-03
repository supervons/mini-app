<template>
  <div class="counter-warp">
    <van-notice-bar
      left-icon="volume-o"
      text="本界面用于展示vuex的一些基础用法，详细用法请参考文档。"
    />
    <p>Vuex counter：{{ count }}</p>
    <p>
      <button @click="increment">+</button>
      <button @click="decrement">-</button>
    </p>
  </div>
</template>

<script>
import { mapState, mapMutations } from 'vuex'

export default {
  computed: {
    ...mapState([
      'count'
    ])
  },

  methods: {
    ...mapMutations([
      'increment',
      'decrement'
    ])
  }
}
</script>

<style>
.counter-warp {
  text-align: center;
  margin-top: 100px;
}
.home {
  display: inline-block;
  margin: 100px auto;
  padding: 5px 10px;
  color: blue;
  border: 1px solid blue;
}
</style>
