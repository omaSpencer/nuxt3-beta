<script lang="ts">
export default {
	layout: 'default',
};
</script>
<script setup lang="ts">
// Server Side Data Fetching
// const { data }: { data: any } = await useFetch('/api/hello?search=girls');
// const { data } = await useAsyncData('searchData', () => $fetch('/api/hello?search=girls'));

import { ref } from 'vue';

const searchText = ref('');
const myData = ref([]) as any;

async function searchForStuff() {
	const data = await fetch(`/api/hello?search=${searchText.value}`);
	const json = await data.json();
	console.log('json', json);
	myData.value = json;
}
</script>
<template>
	<div>
		<form class="form" @submit.prevent="searchForStuff">
			<input type="text" v-model="searchText" />
			<button>Search</button>
		</form>
		<div class="stuff">
			<div v-for="show in myData">
				<img :src="show.show?.image?.medium" alt="" />
			</div>
		</div>
	</div>
</template>

<style>
.stuff {
	margin-top: 50px;
	display: flex;
	justify-content: center;
	align-items: center;
	flex-wrap: wrap;
	/* flex-direction: column; */
	gap: 10px;
}
.form {
	display: flex;
	justify-content: center;
	align-items: center;
	margin-top: 100px;
}
</style>
