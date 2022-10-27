<template>
	<header class="flex align-center mb-1">
		<h2 class="mr-1">{{ currentQuestion }}</h2>
		<div class="icons-wrapper flex align-center gap-1">
			<Icon
				v-if="!isPlaying"
				icon="fa6-solid:circle-play"
				class="icon"
				@click="isPlaying = !isPlaying"
			/>
			<Icon
				v-else
				icon="fa6-solid:circle-pause"
				class="icon"
				@click="isPlaying = !isPlaying"
			/>

			<Icon icon="fa6-solid:circle-stop" class="icon" @click="pauseVoice" />
			<Icon icon="fa6-solid:circle-xmark" class="icon" @click="resetData" />
		</div>
	</header>
	<main class="grid">
		<BaseButton
			@click="currentQuestionNumber++, pauseVoice()"
			v-for="(answer, index) in answers"
			:title="answer"
			:key="index"
		/>
	</main>
</template>

<script>
import BaseButton from "./Button.vue";
import { Icon } from "@iconify/vue";

export default {
	name: "ScreeningQuestions",
	emits: ["next-call"],
	components: {
		BaseButton,
		Icon,
	},
	props: {
		questions: {
			type: Array,
			required: true,
			default: () => ["Question A", "Question B", "Question C", "Question  D"],
		},
		answers: {
			tpye: Array,
			required: true,
			default: () => ["Answer A", "Answer B", "Answer C", "Answer  D"],
		},
		lang: {
			type: String,
		},
	},
	data() {
		return {
			currentQuestionNumber: 0,
			lastQuestionIndex: this.questions.length - 1,
			isPlaying: false,
		};
	},
	computed: {
		currentQuestion() {
			if (this.currentQuestionNumber >= this.questions.length) this.resetData();
			return this.questions[this.currentQuestionNumber];
		},
	},
	methods: {
		resetData() {
			this.currentQuestionNumber = 0;
			this.pauseVoice();
			this.$emit("next-call");
		},
		pauseVoice() {
			if (!this.isPlaying) return;
			this.isPlaying = false;
		},
	},
};
</script>

<style scoped>
.grid {
	display: grid;
	grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
	gap: 1rem;
}

header h2 {
	flex: 1;
}

@media screen and (max-width: 550px) {
	header {
		flex-direction: column;
		align-items: flex-start;
	}
}
</style>
