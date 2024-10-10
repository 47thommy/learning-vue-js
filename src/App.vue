<script>
	export default {
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
		// 	changeStatus() {
		// 		if (this.status === "active") {
		// 			this.status = "pending";
		// 		} else if (this.status === "pending") {
		// 			this.status = "inactive";
		// 		} else {
		// 			this.status = "active";
		// 		}
		// 	},
		// },
	};
</script>

<template>
	<h1>{{ name }}</h1>
	<p v-if="status === 'active'">User account is active</p>
	<p v-else-if="status === 'pending'">User account is in pending status</p>
	<p v-else>User account is InActive</p>

	<ul>
		Tasks:
		<li v-for="(task, index) in tasks" :key="index">{{ task }}</li>
	</ul>
	<a :href="link">Google</a>
	<br />
	<button @click="changeStatus">Change Status</button>
</template>
