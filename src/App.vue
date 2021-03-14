<template>
	<div id="app">
		<h1>Tasks</h1>
		<NewTask @taskAdded="addTask" />
		<TaskProgress v-if="tasks.length" :progress="progress"/>
		<Tasks @deleteTask="deleteTask" @clickedTask="clickedTask" @doneTask="doneTask" :tasks="tasks"/>
	</div>
</template>

<script>
import moment from 'moment'
import Tasks from './components/Tasks'
import NewTask from './components/Tasks/NewTask'
import TaskProgress from './components/Tasks/TaskProgress'

export default {
	components:{ Tasks, NewTask, TaskProgress },
	data() {
	  return {
		task:0,
		tasks:[]
	  }
	},
	watch:{
		tasks:{
			deep:true,
			handler(){
				localStorage.setItem('tasks', JSON.stringify(this.tasks))

			}
		}
	},
	methods: {
		addTask(task){
			const sameName = t => t.name === task.name
			const reallyNew = this.tasks.filter(sameName).length == 0
			reallyNew && this.tasks.push({
				name:task.name,
				pending: task.pending || true,
				created_at:task.created_at,
				done:''
			})		
		},
		clickedTask(i){
			this.tasks[i].pending == true ? this.tasks[i].pending=false : this.tasks[i].pending= true
            // this.tasks[i].pending = tasks[i].pending
			if(this.tasks[i].pending){
				this.tasks[i].done = ''
			}else{
				this.tasks[i].done = moment().format('YYYY/MM/DD HH:mm') 
			}

		},
		doneTask(i){
		},
		deleteTask(task){
			this.tasks.splice(task, 1)
		}
	},
	computed: {
		progress(){
			const total = this.tasks.length
			const done = this.tasks.filter(f=> !f.pending).length

			return Math.round(done/total *100) || 0
		}
	},
	created(){
		const json = localStorage.getItem('tasks')
		this.tasks = JSON.parse(json) || []
	}
}
</script>

<style>
	body {
		font-family: 'Lato', sans-serif;
		background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
		color: #FFF;
	}

	#app {
		display: flex;
		flex: 1;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		height: 100vh;
	}

	#app h1 {
		margin-bottom: 5px;
		font-weight: 300;
		font-size: 3rem;
	}
</style>
