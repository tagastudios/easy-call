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
	border: 2px ridge var(--secondary-color);
	background-color: var(--primary-color);
	color: white;
	font-size: 1rem;
	font-weight: 700;
	text-transform: capitalize;
	transition: all 0.35s ease-in-out;
}

.baseButton:hover {
	background-color: var(--secondary-color);
}
</style>
