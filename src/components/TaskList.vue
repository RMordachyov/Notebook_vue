<template >
    <div class="task-list-container">
        <div class="summary">
            <p>Всего задач: {{ getTaskCount }}</p> 
            <p>Выполнено: {{ getCompleteTask }}</p>
        </div> 
        <TaskForm @addTask="addTask"/> 
        <div class="tasks-content">
            <task v-for="(task,index) in Tasks" :task="task" :key="index" @deleteTask="deleteTask">
                <template v-slot:header>
                    <h3>Заметка по задаче "{{ task.title }}"</h3>
                </template>
                <template v-slot:main>
                    <p>{{ task.description }}</p>
                </template>
                
            </task>
        </div>  
             
    </div>
    
</template>

<script>
import Task from "../components/Task.vue"
import TaskForm from '../components/TaskForm.vue'

export default{
    data(){
    return{
      TaskCount:0,
      completeTask: 0,
      Tasks:[
        {
          id:"1", 
          title:"task 1", 
          description:"description task 1",
          completed:"In progress"
        },
        {
          id:"2", 
          title:"task 2", 
          description:"description task 2",
          completed:"In progress"
        }
      ]
    }
  },
  computed:{
    getTaskCount(){
      return this.Tasks.length
    },
    getTasks(){
        return this.Tasks
    },
    getCompleteTask(){
        this.completeTask = (this.Tasks.filter(e => e.completed == 'Done')).length;
        return this.completeTask
    }
  },
  methods:{
    addTask(data){
      this.Tasks.push({id: this.Tasks.length+1, title: data[0], description: data[1], completed: "In progress"})
    },
    deleteTask(id){
        let obj = this.Tasks.find(e => e.id === id);
        let i = this.Tasks.indexOf(obj);
        if(i >= 0) {
            this.Tasks.splice(i,1);
        }
    }
  },
  components:{
    Task,
    TaskForm
  }
}
</script>

<style lang="scss">
.task-list-container{
    position: relative;
}
.tasks-content{
    display: flex;
    align-items: center;
    justify-content:flex-start;
    flex-wrap: wrap;
}
.summary{
    position: absolute;
    right: 20px;
    top: 0;
    border-radius: 15px;
    box-shadow: 0 0px 5px rgba($color: #000000, $alpha: 0.20);
    padding: 15px;
}
.summary p:first-child{
    margin-bottom: 10px;
    color: rgb(255, 145, 0);
}
.summary p:last-child{
    color: rgb(0, 155, 34);
}
</style>