<template>
  <main>

    <!-- heading -->
    <header>
      <img src="./assets/logo.svg" alt="pinia logo">
      <h1>{{ taskStore.name }}</h1>
    </header>

    <!-- new task form -->
    <div class="new-task-form">
      <TaskForm />
    </div>

    <!-- filter -->
    <nav class="filter">
      <button @click="filter = 'all'">All tasks</button>
      <button @click="filter = 'favs'">Fav tasks</button>
    </nav>

    <!-- loading -->
    <div class="loading" v-if="taskStore.loading">Loading Tasks...</div>

    <!--task list-->
    <div class="task-list" v-if="filter === 'all'">
      <p class="all">Your have {{taskStore.totalCount}} tasks left to do</p>
      <hr />
      <div v-for="task in taskStore.tasks" :key="task">
        <TaskDetails :task="task" />
      </div>
    </div>
    <div class="task-list" v-if="filter === 'favs'">
      <p class="all">Your have {{taskStore.favCount}} favs left to do</p>
      <hr />
      <div v-for="task in taskStore.favs" :key="task">
        <TaskDetails :task="task" />
      </div>
    </div>
  </main>
</template>

<script>
import { ref } from '@vue/reactivity'
import TaskDetails from './components/TaskDetails.vue'
import TaskForm from '@/components/TaskForm.vue'
import { useTaskStore } from './stores/TaskStore'

  export default {
    components: { TaskDetails, TaskForm },
    setup(){

      const taskStore = useTaskStore()


      //fetch tasks
      taskStore.getTasks()

      const filter = ref('all')

      return { taskStore, filter }
    }
  }
</script>
