<script setup>
	import { ref, onMounted, defineProps, defineEmits } from "vue";
	const boxes = defineProps({ checkBoxList: Object });
	const selected = ref([]);
	onMounted(() => boxes.checkBoxList.seleted.forEach((val) => setSelected(val)));
	const setSelected = (val) => {
		if (selected.value.includes(val)) {
			document.getElementById(val + "-Box").innerHTML = "";
			const index = selected.value.indexOf(val);
			selected.value.splice(index, 1);
		} else {
			document.getElementById(val + "-Box").innerHTML = "✔";
			document.getElementById(val + "-Box").style.display = "flex";
			document.getElementById(val + "-Box").style.justifyContent = "center";
			document.getElementById(val + "-Box").style.alignItems = "center";
			selected.value.push(val);
			selected.value = [...new Set(selected.value)];
		}
		onChange(selected.value);
	};
	const emit = defineEmits(["onChange"]);
	function onChange() {
		emit("onChange", selected.value);
	}
</script>

<template>
	<div
		v-for="(box, index) of boxes.checkBoxList.countries"
		:key="index"
		style="float: left; padding-right: 50px">
		<div style="display: flex; padding: 15px 0 0 15px; flex-direction: row">
			<div
				@click="()=>{
                   boxes.checkBoxList?.disableAll==true?undefined:!box?.isDisabled?setSelected(box.label):undefined
                }
             "
				:id="box.label + '-Box'"
				style="width: 15px; height: 15px; background: silver; margin-right: 10px; border: 2px solid skyblue; padding: 1px"></div>
			<div style="font-family: arial; color: black">{{ box.label }}</div>
		</div>
	</div>
</template>

<style scoped>
	button {
		font-weight: bold;
	}
</style>
