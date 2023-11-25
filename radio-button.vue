<script setup>
	import { ref, onMounted, defineProps, defineEmits } from "vue";
	const radios = defineProps({ radioButton: Object });
	const selected = ref(radios.radioButton.seleted);

	onMounted(() => setSelected(selected.value));
	const setSelected = (val) => {
		document.getElementById(val + "-Radio").style.background = "black";
		selected.value = val;
		const rad = radios.radioButton.countries.filter((radio) => radio.label != val);
		rad.forEach((r) => {
			document.getElementById(r.label + "-Radio").style.background = "silver";
		});
		onChange(selected.value);
	};
	const emit = defineEmits(["onChange"]);
	function onChange() {
		emit("onChange", selected.value);
	}
</script>

<template>
	<div
		v-for="(radio, index) of radios.radioButton.countries"
		:key="index"
		style="float: left; padding-right: 50px">
		<div style="display: flex; padding: 15px 0 0 15px; flex-direction: row">
			<div
				@click="
					() => {
						radio.isDisabled ? undefined : setSelected(radio.label);
					}
				"
				:id="radio.label + '-Radio'"
				style="width: 15px; height: 15px; background: silver; border-radius: 50%; margin-right: 10px; border: 2px solid skyblue; padding: 1px"></div>
			<div style="font-family: arial; color: rgb(43, 39, 39)">{{ radio.label }}</div>
		</div>
	</div>
</template>

<style scoped>
	button {
		font-weight: bold;
	}
</style>

