<template>
  <div class="task-grid"> 
    <template v-if="tasks.length">
      <Task v-for="(task, i) in tasks"  @deleteTask="$emit('deleteTask', i)" @clickedTask="$emit('clickedTask', i)"  @doneTask="$emit('doneTask', i)" :key="task.name" :task="task">

      </Task>
    </template>
    <p v-else class="no-task">Your life is up to date</p>
  </div>
</template>

<script>
import Task from './Task'
export default {
  props:{
    tasks:{
      type: Array, required:true
    }
  },
  components:{
    Task,
  },
  data() {
    return {
      todo:"",
      valueDeterminate:50,
    }
  },
};
</script>

<style>
  .task-grid {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
  }
  .task-grid .task {
    margin: 10px;
  }
  .no-task{
    font-size: 1.7rem;
    color: #AAA;
  }
</style>