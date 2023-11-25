<!-- @format -->

<template>
	<div class="hello">
		<el-form
			@submit.prevent="disp"
			style="padding: 1rem; display: flex; flex-direction: column">
			<h4>Custom Radio Buttons</h4>
			<RadioButton
				:radioButton="radioButton"
				@onChange="radioButtonValue" />
			<h4>Custom CheckBoxes</h4>

			<CheckBox
				:checkBoxList="checkBoxList"
				@onChange="checkBoxValue" />
			<h4>Custom ListBox</h4>

			<ListBox
				:listData="listData"
				@onClick="ListBoxValue" />

			<button
				type="submit"
				id="button">
				Login
			</button>
		</el-form>
		<fieldset>
			<h5>Radio Button Selected : {{ radioButtonSeleted }}</h5>
			<div>
				<h5>CheckBoxes Selected</h5>
				<ul
					v-for="(checkbox, index) of checkBoxesSeleted"
					:key="index">
					<li>{{ checkbox }}</li>
				</ul>
			</div>
			<div>
				<h5>ListBox Selected</h5>
				<ul
					v-for="(listbox, index) of listBoxesSeleted"
					:key="index">
					<li>{{ listbox }}</li>
				</ul>
			</div>
		</fieldset>
	</div>
</template>

<script>
	import { ref, reactive } from "vue";
	import RadioButton from "./custom-components/radio-button.vue";
	import CheckBox from "./custom-components/check-box.vue";
	import ListBox from "./custom-components/list-box.vue";
	export default {
		components: { RadioButton, CheckBox, ListBox },
		name: "Testing",

		setup() {
			const radioButtonSeleted = ref("");
			const checkBoxesSeleted = ref([]);
			const listBoxesSeleted = ref([]);
			const radioButton = {
				countries: [
					{ label: "Pakistan", isDisabled: true },
					{ label: "India", isDisabled: false },
					{ label: "Bangldesh", isDisabled: true },
					{ label: "Nepal", isDisabled: false },
					{ label: "China", isDisabled: true }
				],
				seleted: "Pakistan"
			};
			const checkBoxList = {
				countries: [{ label: "Pakistan", isDisabled: true }, { label: "India", isDisabled: false }, { label: "Bangldesh", isDisabled: true }, { label: "Nepal", isDisabled: false }, { label: "China", isDisabled: true }, { label: "USA" }],
				seleted: ["Pakistan"],
				disableAll: false
			};
			const listData = {
				list: [
					{ label: "Pakistan", isDisabled: true },
					{ label: "India", isDisabled: false },
					{ label: "Bangldesh", isDisabled: true },
					{ label: "Nepal", isDisabled: false },
					{ label: "China", isDisabled: true }
				],
				disableAll: false,
				slected: ["Nepal", "China"]
			};

			function radioButtonValue(value) {
				console.log(value);
				radioButtonSeleted.value = value.toString();
			}
			function checkBoxValue(value) {
				checkBoxesSeleted.value = [...value];
				console.log(value);
			}

			function ListBoxValue(value) {
				listBoxesSeleted.value = [...value.value];
				console.log(value.value);
			}
			return reactive({
				radioButton,
				radioButtonValue,
				checkBoxValue,
				checkBoxList,
				radioButtonSeleted,
				checkBoxesSeleted,
				ListBox,
				listData,
				ListBoxValue,
				listBoxesSeleted
			});
		}
	};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	.hello {
		display: flex;
		justify-content: center;
		align-items: center;
		margin-top: 1%;
		box-sizing: border-box;
		padding: 0%;
		display: flex;
		margin: 0 auto !important;
	}
	label {
		font-size: x-large;
	}

	#button {
		background-color: #00b4d8;
		color: white;
		font-weight: bold;
		font-size: 1.5rem;
		padding: 14px 20px;
		margin: 8px 0;
		border: none;
		cursor: pointer;
		width: 94%;
	}

	button:hover {
		opacity: 0.8;
	}
	fieldset {
		background: rgba(255, 255, 255, 0.25);
		box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
		backdrop-filter: blur(4px);
		-webkit-backdrop-filter: blur(4px);
		border-radius: 10px;
		border: 1px solid rgba(255, 255, 255, 0.18);
	}

	fieldset:hover,
	fieldset:focus {
		box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
	}
</style>
