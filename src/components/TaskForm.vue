<template>
    <div class="createForm">
        <form>
            <label for="title">Заголовок</label>
            <input type="text" name="title" v-model="title"><br>
            <label for="description">Описание</label>
            <input type="text" name="description" v-model="description"><br>
            
        </form>
        <button @click="createTaskElement" class="button-addTask">Добавить задачу</button>
    </div>
</template>

<script>
export default{
    data(){
        return{
            title:"",   
            description:""
        }  
    },
    methods:{
        createTaskElement(){
            let inpTitle = document.querySelector('[name="title"]')
            let inpDescription = document.querySelector('[name="description"]')
            if(this.title == ''){
                alert('Не заполнено поле "Заголовок"')
                inpTitle.focus()
                return '';
            }
            if(this.description == ''){
                alert('Не заполнено поле "Описание"')
                inpDescription.focus()
                return '';
            }
            this.$emit('addTask', [this.title, this.description])
        }
    },
    components:{
        
    }
}
</script>

<style scoped>
.createForm{
    width: 300px;
    margin: 15px auto;
}
input{
    width: 100%;
    margin-bottom: 15px;
    height: 30px;
    border-radius: 5px;
    border: 1px solid #C0C0C0;
    padding: 3px 10px;
}

input:focus{
    outline: none;
}

.button-addTask{
    width: 100%;
    border: 0;
    color: white;
    font-weight: bold;
    background-color: #16cebed2;
    border-radius: 5px;
    padding: 10px 25px;
    text-transform: uppercase;
}
</style>