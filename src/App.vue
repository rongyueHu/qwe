<template>
  <section class="todoapp">
    <!-- 除了驼峰, 还可以使用-转换链接 -->
    <TodoHeader @add-event="add" :list="list"></TodoHeader>
    <TodoMain @del-event="del" :arr="showArr"></TodoMain>
    <TodoFooter
      @clear-event="clear"
      @change="changeType"
      :far="showArr"
    ></TodoFooter>
  </section>
</template>

<script>
// 1.0 样式引入
import "./styles/base.css"
import "./styles/index.css"
import TodoHeader from "./components/TodoHeader";
import TodoMain from "./components/TodoMain";
import TodoFooter from "./components/TodoFooter";
export default {
  data () {
    return {
      list: JSON.parse(localStorage.getItem('todolist')) || [],
      getSel: 'all'
    }
  },
  methods: {
    del (Id) {
      const index = this.list.findIndex(item => item.id === Id)
      this.list.splice(index, 1)
    },
    add (Name) {
      let id = this.list.length === 0 ? 100 : this.list[this.list.length - 1].id + 1
      this.list.push({
        id: id,
        name: Name,
        isDone: false
      })
    },
    changeType (str) {
      this.getSel = str
    },
    clear () {
      this.list = this.list.filter(item => item.isDone === false)
    }
  },
  computed: {
    showArr () {
      if (this.getSel === 'yes') {
        return this.list.filter(item => item.isDone === true)
      } else if (this.getSel === 'no') {
        return this.list.filter(item => item.isDone === false)
      } else {
        return this.list
      }
    }
  },
  watch: {
    list: {
      deep: true,
      handler () {
        localStorage.setItem('todolist', JSON.stringify(this.list))
      }
    }
  },
  components: {
    TodoHeader,
    TodoMain,
    TodoFooter,
  },
};
</script>