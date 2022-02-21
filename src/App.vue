<template>
  <main>
    <TaskInput @onAddTask="addTask"></TaskInput>
    <ul class="task-list my-list">
      <li v-for="item in TaskList" :key="item.id">
        <TaskCard @onRemove="removeTask(item.id)" @onDone="setDoneTask(item.id)" :model="item"></TaskCard>
      </li>
    </ul>
    

  </main>
</template>

<script>
import TaskInput from "./components/TaskInput.vue"
import TaskCard from "./components/TaskCard.vue";
import {ref} from 'vue'
export default {
  name: 'App',
  components: {
    TaskCard,
    TaskInput
  },
  setup(){
    const TaskList = ref([{id: 0, title: 'create video', description: 'upload on YT', status:false}])
    const addTask = ({title, description}) => {
      TaskList.value = [...TaskList.value, {id:TaskList.value.length+1, title, description, status:false}]
    }
    const setDoneTask = (id) => {
      TaskList.value = TaskList.value.map(x => {
        if(x.id == id){
          x.status = true
        }
        return x
      })
    }
    const removeTask = (id) => {
      TaskList.value = TaskList.value.filter(x => x.id != id)
    }
    return {
      TaskList,
      addTask,
      removeTask,
      setDoneTask
    }
  }
}
</script>

<style scoped>
  .task-list{
    list-style: none;
  }
</style>
