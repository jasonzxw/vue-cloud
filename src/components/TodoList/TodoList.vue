<script>
import { reactive  ,ref} from 'vue'
export default {
    setup() {
        const list = reactive([]);
        const val = ref('');
        // watch(val , () => {
        //     list.push(val.value);
        //     val.value = ''
        // });

        const addTodo = () => {
            if(val.value){
                list.push(val.value);
                val.value = ''
            }
        }

        const doneList = (index) =>{
            list.splice(index,1)
        }
        return {
            list,
            val,
            addTodo,
            doneList
        }
    },
}
</script>

<template>
    <div>
        <input v-model="val"/> <button @click="addTodo">add</button>
        <div v-for="(item,index) in list" :key="item" >
            <span>{{item}}</span> <button @click="doneList(index)">Done</button>
        </div>
    </div>
</template>