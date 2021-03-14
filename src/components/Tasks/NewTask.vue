<template>
  <div class="new-task">
    <v-row>
        <input  class="form-element" @keydown.enter="add" v-model="name">
        <button class="form-element"  @click="add">
            +
            <!-- <v-icon large >mdi-plus</v-icon> -->
        </button>
        
    </v-row>
  </div>
</template>

<script>
import moment from 'moment'
export default {
    data() {
        return {
            name:''
        }
    },
    methods: {
        add(){
            
            const created_at = moment().format('YYYY/MM/DD HH:mm')
            if(this.name){
                this.$emit('taskAdded', {name:this.name, created_at })
                this.name = ''
            }
        }
    },
}
</script>

<style>
    .new-task {
        margin: 35px;
    }
    .form-element {
        outline: none  ;
        font-size: 2rem ;
        border: 1px solid #fff ;
        padding: 5px 10px 8px ;
        
    }
     input.form-element {
        width: 500px  ;
        background: #fff2 ;
        color: #DDD;
        border-top-left-radius: 8px;
        border-bottom-left-radius: 8px ;
    }
    button.form-element {
        border-left: none ;
        background: #2196f3 ;
        border-top-right-radius: 8px ;
        border-bottom-right-radius: 8px ;
    }

</style>