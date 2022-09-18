<template>
  <header class="header">
    <h1>todos</h1>
    <input id="toggle-all" class="toggle-all" v-model="isAll" type="checkbox" />
    <label for="toggle-all"></label>
    <input
      @keydown.enter="addFn(task)"
      v-model="task"
      class="new-todo"
      placeholder="输入任务名称-回车确认"
      autofocus
    />
  </header>
</template>

<script>
export default {
  props: ['list'],
  data () {
    return {
      task: ''
    }
  },
  methods: {
    addFn () {
      this.$emit('add-event', this.task)
      this.task = ''
    }
  },
  computed: {
    isAll: {
      set (checked) {
        this.list.forEach(item => item.isDone = checked)
      },
      get () {
        return this.list.length !== 0 && this.list.every(item => item.isDone === true)
      }
    }
  }

}
</script>