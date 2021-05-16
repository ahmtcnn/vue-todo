<template>
  <div class="home">

    <v-text-field
            v-model="newTaskTitle"
            @keyup.enter="addTask"
            outlined
            label="Add Task"
            append-icon="mdi-plus"
            class="pa-3"
            hide-details
            clearable
            @click:append="addTask"
          ></v-text-field>

    <v-list
      flat
      class="pt-0"
    >

        <div v-for="task in tasks" :key="task.id">

        <v-list-item
        @click="doneTask(task.id)"
        :class="{'blue lighten-5' : task.done }">

          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="task.done"></v-checkbox>
              
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
              :class="{ 'text-decoration-line-through' : task.done}"
              >{{task.title}}</v-list-item-title>
            </v-list-item-content>
      <v-list-item-action>
          <v-btn 
          @click.stop="deleteTask(task.id)"
          icon>
            <v-icon color="primary lighten-1">mdi-delete</v-icon>
          </v-btn>
      </v-list-item-action>
          </template>
        </v-list-item>
        <v-divider></v-divider>
        </div>






    </v-list>
  </div>
</template>

<script>


  export default {
    name: 'Home',

    components: {

    },
    data(){
     return{
       newTaskTitle : '',
       tasks: [
        //  {
        //    id:1,
        //    title: "Wake up",
        //    done: false,

        // },
        //  {
        //    id:2,
        //    title: "Homework",
        //    done: false


        // },
        //  {
        //    id:3,
        //    title: "Sport",
        //    done: false

        // }
       ]
     }
    },
    methods : {
      doneTask(id){
        let task = this.tasks.filter(task => task.id === id)[0]
        console.log(task)
        task.done = !task.done
        console.log(task)
      },
      deleteTask(id){
        this.tasks = this.tasks.filter(task => task.id !== id)
      },
      addTask(){
        let newTask = {
          id: Date.now(),
          title : this.newTaskTitle,
          done : false
        }
        this.tasks.push(newTask)
        this.newTaskTitle = null
      }
    }
  }
</script>
