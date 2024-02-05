<template>
  <main>
    <h1>Добро пожаловать!</h1>
    <div class="container">
      <TaskList />
    </div>

  </main>
</template>

<script>
import TaskList from '../components/TaskList.vue'
export default{
  components:{
    TaskList
  },
  methods:{
    
  }
}
</script>

<style lang="scss">
h1{
  text-align: center;
  margin: 20px auto;
  padding-top: 20px;
}
  main{
    width: 800px;
    height: 100%;
    // border: 1px solid #000;
    margin: auto;
    background-color: white;
    border-radius: 15px;
    margin-top: 25px;
    box-shadow: 0 0px 20px rgba($color: #000000, $alpha: 0.30);
  }
</style>