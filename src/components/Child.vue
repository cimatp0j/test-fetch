<template>
	<h4>Child</h4>
	<div v-for="(path, i) in paths" :key="i">
		<div>{{ path }}:{{ data[i] }}</div>
	</div>
</template>

<script setup>
import { ref, toRef, watch } from 'vue';

const props = defineProps({ //eslint-disable-line
	stat: {
		type: Object,
		required: true,
		default: () => ({
			paths: [],
			data: [],
		})
	}
});

const stat = toRef(props, 'stat');
const paths = ref([]);
const data = ref([]);

watch(props, () => {
	console.log('child')
	console.log(props.stat)
	paths.value = stat.value.paths
	data.value = stat.value.data
	console.log(props.stat.paths)
	console.log(props.stat.data)
	console.log(paths.value)
	console.log(data.value)
	console.log('child-end')
})


</script>
