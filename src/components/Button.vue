<template>
	<div class="baseButton">
		<slot name="default">{{ title }}</slot>
	</div>
</template>

<script setup>
defineProps({
	title: {
		type: String,
		default: "Default Title",
	},
});
</script>

<style scoped>
.baseButton {
	border-radius: 10px;
	padding: 0.5rem 1rem;
	border: 2px ridge rebeccapurple;
	background-color: rgb(158, 91, 224);
	color: white;
	font-size: 1rem;
	font-weight: 700;
	text-transform: capitalize;
}
</style>
