<template>
  <div class="row">
    
      <h1> My to do app</h1>
  <!-- v-bind:src raccourci :src  -->
  
  
  <!-- count tasks -->
  <!-- task for 1 and tasks for many  -->
  <h4> you have {{ allTasks }} {{ allTasks > 1 ? 'tasks' : 'task' }} at the moment</h4>
  <div class="input-group mb-3">
    <input type="text" v-model="newTask" class="form-control" @keyup.enter="addTask" placeholder="your new task" >
    <!-- v-on=click in @click  -->
    <button class="btn btn-success" @click="addTask" :disabled="newTask.length < 1">add your task</button>
  </div>
  
  <!-- <h2> new task </h2>

  <div v-if="newTask.length > 0">
    {{ newTask }}
  </div> -->

<h2> new to old task </h2>
<p>click on the task if you are done with</p>


  <table class="table table-bordered">
    <!-- reverse the list -->
    <tr>
      <td> order </td>
      <td> name </td>
      <td> delete </td>
    </tr>
    <tr v-for="(task, index) in latest" :key="task.id" @click="finishTask(task)" :class="{ strikeout: task.finished }">
      <td>{{ index + 1 }}</td>
      <td>{{ task.name }}</td>
     <td type="button" @click="removeTask(task.id)" class="btn btn-danger"> delete </td>
    </tr>
  </table>
      <!-- v-for for looping -->
            <!-- <li v-for = "task in tasks" :key="task.id">
                {{ task.id}}. {{ task.name }} -->

            <!-- v-if for conditional  -->
          

    </div>
    
 
</template>

<script>
    export default {
  data() {
    return {
      newTask: '',
      // array of object
      tasks: []
    }
  },

//   changing data
  methods: {
    addTask() {
      if (this.newTask.length < 1) return
        this.tasks.push({
          id: this.tasks.length + 1,
          name: this.newTask,
          finished: false
        });

        this.newTask = ''
    },
    finishTask(task) {
        task.finished = !task.finished
    },
    removeTask(taskID) {
        this.tasks = this.tasks.filter( task => {
            return task.id !== taskID
        })
    }
  },

//   propriété calculées toujours avec "return"
// showing data
  computed: {
    allTasks() {
        return this.tasks.length
    },
    latest() {
        return [...this.tasks].reverse()
    }
  }

}
</script>
