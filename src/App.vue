<script setup>
	import { ref, onMounted } from "vue";

	//  this is using options api
	// data() {
	// 	return {
	// 		name: "Thomas Wondwosen",
	// 		status: "inactive",
	// 		tasks: ["task one", "task two", "task three", "task four", "task five"],
	// 		link: "https://google.com",
	// 	};
	// },
	// methods: {
	// changeStatus() {
	// 	if (this.status === "active") {
	// 		this.status = "pending";
	// 	} else if (this.status === "pending") {
	// 		this.status = "inactive";
	// 	} else {
	// 		this.status = "active";
	// 	}
	// },
	// },

	const name = ref("Thomas Wondwosen");
	const status = ref("inactive");
	const tasks = ref([
		"task one",
		"task two",
		"task three",
		"task four",
		"task five",
	]);
	const newTask = ref("");
	const link = "https://google.com";

	const changeStatus = () => {
		if (status.value === "active") {
			status.value = "pending";
		} else if (status.value === "pending") {
			status.value = "inactive";
		} else {
			status.value = "active";
		}
	};

	const addNewTask = () => {
		if (newTask.value !== "") {
			tasks.value.push(newTask.value);
			newTask.value = "";
		}
	};
	const deleteTask = (index) => {
		tasks.value.splice(index, 1);
	};

	onMounted(async () => {
		const response = await fetch("https://jsonplaceholder.typicode.com/todos");
		const data = await response.json();
		tasks.value = data.map((task) => task.title);
	});
</script>

<template>
	<h1>{{ name }}</h1>
	<p v-if="status === 'active'">User account is active</p>
	<p v-else-if="status === 'pending'">User account is in pending status</p>
	<p v-else>User account is InActive</p>

	<ul>
		Tasks:

		<li v-for="(task, index) in tasks" :key="index">
			<span>
				{{ task }}
			</span>
			<button @click="deleteTask(index)">x</button>
		</li>
	</ul>
	<a :href="link">Google</a>
	<br />
	<button @click="changeStatus">Change Status</button>

	<form @submit.prevent="addNewTask">
		<label for="addTask">Add Task</label>
		<input type="text" id="addTask" name="addTask" v-model="newTask" />
		<button type="submit">Add Task</button>
	</form>
</template>
