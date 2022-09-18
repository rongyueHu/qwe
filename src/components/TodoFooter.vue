<template>
  <footer class="footer">
    <span class="todo-count"
      >剩余<strong>{{ count }}</strong></span
    >
    <ul class="filters" @click="fn">
      <li>
        <a
          @click="isSel = 'all'"
          :class="{ selected: isSel === 'all' }"
          href="javascript:;"
          >全部</a
        >
      </li>
      <li>
        <a
          @click="isSel = 'no'"
          :class="{ selected: isSel === 'no' }"
          href="javascript:;"
          >未完成</a
        >
      </li>
      <li>
        <a
          @click="isSel = 'yes'"
          :class="{ selected: isSel === 'yes' }"
          href="javascript:;"
          >已完成</a
        >
      </li>
    </ul>
    <button @click="clearFn" class="clear-completed">清除已完成</button>
  </footer>
</template>

<script>
export default {
  props: ['far'],
  data () {
    return {
      isSel: 'all' //all全部 yes是 no否
    }
  },
  computed: {
    count () {
      return this.far.length
    }
  },
  methods: {
    fn () {
      this.$emit('change', this.isSel)
    },
    clearFn () {
      this.$emit('clear-event')
    }
  }
}
</script>