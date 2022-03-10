<template>
	<h3>Parent</h3>
	<Child :stat="stat" />
</template>

<script setup>
import { ref, onMounted } from 'vue';
import Child from '@/components/Child.vue';

const stat = ref({})

const getStatus = (urls) => {
	const results = {};
	results.paths = urls;
	const promises = urls.map(url => fetch(url));
	Promise.allSettled(promises).then(resp => {
		results['data'] = resp.map(r => {
			if (r.status === "fullfilled"){
				if(r.value.ok){
					return 'OK';
				} else {
					return 'NG';
				}
			} else {
				return 'ERROR';
			}
		});
	});
	return results;
}

onMounted(() => {
	const urls = [
		'https://httpbin.org/status/200', // OK
		'https://httpbin.org/status/404', // NG
	];
	stat.value = getStatus(urls);
	console.log('parent')
	console.log(stat.value)
	console.log(stat.value.paths)
	console.log(stat.value.data)
	console.log('parent-end')
});

</script>
