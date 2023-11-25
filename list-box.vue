<script setup>
	import { ref, defineProps, defineEmits, onMounted } from "vue";
	const data = defineProps({
		listData: Object
	});
	const list = ref(data.listData.list);
	const selectedList = ref([]);
	onMounted(() => data.listData.slected.forEach((value) => onClick(value)));
	const emit = defineEmits(["onClick"]);
	function onClick(value) {
		if (selectedList.value.includes(value)) {
			const index = selectedList.value.indexOf(value);
			selectedList.value.splice(index, 1);
			document.getElementById(value).style.background = "";
		} else {
			selectedList.value.push(value);
			document.getElementById(value).style.background = "#EBE3D5";
		}
		emit("onClick", selectedList);
	}
</script>
<template>
	<ul
		v-for="l of list"
		:key="l">
		<li
			:id="l.label"
			@click="() => (data.listData.disableAll == true ? undefined : l.isDisabled ? undefined : onClick(l.label))">
			{{ l.label }}
		</li>
	</ul>
</template>
<style scoped>
	ul,
	li {
		list-style: none;
		padding: 1px 3px;
		margin: 0%;
		text-align: left;
	}
	li {
		border-bottom: 1px solid #c7c7c4;
	}
</style>

