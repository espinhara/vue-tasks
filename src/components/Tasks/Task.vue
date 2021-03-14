<template>
  <div class="task"  @click=" $emit( 'clickedTask', task)" :class="stateClass">
    <template v-if="task.pending">
        <span class="close" @click="$emit('deleteTask', task)">
            <v-icon large >mdi-delete-circle</v-icon>
        </span>
        <p>{{task.name}}</p>
        <span class="created" >
            Created: {{task.created_at}}
        </span>
    </template>
    <template v-else>
        <span class="close" @click="$emit('deleteTask', task)">
            <v-icon large >mdi-delete-circle</v-icon>
        </span>
        <p>{{task.name}}</p>
        <span class="done-date" >
            Done: {{task.done}}
        </span>
    </template>
  </div>
</template>

<script>
export default {
    props:{
        task:{
            type: Object,
            required: true,
        }
    },
    methods: {
        clickedTask(task){
            task.pending == true ? task.pending=false : task.pending= true
            this.task.pending = task.pending
            // this.$emit('doneTask', task )
            
        }
    },
    computed: {
        stateClass(){
            return{
                pending:this.task.pending,
                done: !this.task.pending
            }
        }
    },
}
</script>

<style>
    .task{
        position: relative;
        box-sizing: border-box;
        height: 150px;
        width: 350px;
        padding: 10px;
        border-radius: 8px;
        font-size: 2rem;
        font-weight: 300;
        cursor: pointer;
        user-select: none;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .pending{
        border-left: 12px solid #ec3929;
        background-color: #da736a;
    }
    span.done-date{
        position: absolute;
        left: 10px;
        bottom: 10px;
        font-size: 1.2rem;
        font-weight: 500;
        font-style: italic;
        color: #26da8c;
    }
    span.created{
        position: absolute;
        left: 10px;
        bottom: 10px;
        font-weight: 500;
        font-style: italic;
        font-size: 1.2rem;
        color: #ec3929;
    }
    .close{
        position: absolute;
        right: 10px;
        top: 10px;
        color: #ec3929;
    }
    .done{
        color:rgb(204, 197, 197);
        border-left: 12px solid #26da8c;
        background-color: #89f3ce;
        text-decoration: line-through;
    }
</style>