<template>
    <div class="task" v-bind:class = "(task.completed == 'Done')?'task done':'task in-progress'">
        <h4>Задача {{ task.title }}</h4>  
        <p> Текущий статус: <i>{{ task.completed }}</i></p>
        <label for="checkStatus">Выполнено </label>
        <input type="checkbox" @change="setStatus" v-model="checked" name="checkStatus"><br>
        <button @click="showDescription" class="button-info">Подробнее</button>
        <button @click="deleteTask" class="button-delete">Удалить</button>
            <div v-show="show">
                <div class="modal-bg active" id="modal-bg"  @click="closeDescription">
                <div class="m-body">
                    <div class="close"  @click="closeDescription">&times;</div>
                    <slot name="header"></slot>
                    <hr>
                    <div class="m-body-content">
                    <slot name="main"></slot>
                    </div>
                    
                </div>
                </div>
            </div>
    </div>
</template>

<script>
export default{
    data(){
        return{
            checked: false,
            show: false
        }
    },
    props:[
        'task'
    ],
    methods:{
        deleteTask(){
            this.$emit('deleteTask', this.task.id)
        },
        setStatus(){
            if(this.checked){
                return this.task.completed = 'Done'
            }else{
                return this.task.completed = 'In progress'
            }
        },
        showDescription(){
            this.show = true
        },
        closeDescription(){
            this.show = false
        }
    }
}
</script>

<style lang="scss">
.task{
    width: 250px;
    margin: 8px;
    padding: 20px;
    border-radius: 15px;
    box-shadow: 0 0px 5px rgba($color: #000000, $alpha: 0.30);
}

.in-progress{
    background-color:#ee752570;
}

.done{
    background-color:#25ee46ab;
}

button{
    margin-top: 15px;
}

.button-info{
    width: 100%;
    border: 0;
    color: white;
    font-weight: bold;
    background-color: #1ca6f7;
    border-radius: 5px;
    padding: 10px 25px;
    text-transform: uppercase;
}

.button-delete{
    width: 100%;
    border: 0;
    color: white;
    font-weight: bold;
    background-color: #EB321F;
    border-radius: 5px;
    padding: 10px 25px;
    text-transform: uppercase;
}

.modal-bg{
    position: fixed;
    top:0;
    bottom: 0;
    left: 0;
    right: 0;
    background: rgba(0, 0, 0, 0.15);
    display: block;
    
}

.modal-bg.active{
    display: flex;
}

.m-body{
    background: white;
    padding: 20px;
    border-radius: 5px;
    max-width: 310px;
    min-height: 200px;
    position: relative;
    margin: auto;
}

.m-body-content{
    margin: 10px auto;
    padding: 5px;
}

.close{
    position: absolute;
    right: 10px;
    top: 5px;
    cursor: pointer;
    z-index: 1;
}
</style>