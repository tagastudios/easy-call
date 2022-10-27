<script setup>
	import LanguageSelector from "./components/LanguageSelector.vue";
	import ScreeningQuestions from "./components/ScreeningQuestions.vue";
	import CallCounter from "./components/CallCounter.vue";
	import MusicPlayer from "./components/MusicPlayer.vue";
	// import { PrismaClient } from "@prisma/client";
	import { ref } from "vue";

	const lang = ref("eng");
	const callCount = ref(0);
	const goal = 250;

	// const prisma = new PrismaClient();

	const questions = {
		esp: [
			"Estaba haciendo una encuesta a ver si me ayuda?",
			"Cual es su principal preocupacion",
			"Yadira Caraveo",
			"Jena Griswald",
		],
		eng: [
			`I'm doing a short survey, can you help?`,
			`What's the main concern?`,
			"Yadira Caraveo",
			"Jena Griswald",
		],
	};

	const answers = {
		esp: {
			agradecido: "./assets/audio/eng/espA1.m4a",
			penoso: `Ohh lamento escuchar eso`,
			"de acuerdo": "Entiendo perfectamente",
		},
		eng: {
			thankfull: "Thank you!!",
			petty: `Ohh I'm sorry to hear that`,
			aggreable: "I totally understand",
		},
	};

	const nextCall = () => {
		callCount.value++;
	};
</script>

<template>
	<header class="mb-3">
		<h1>Easy Call System - v1.0</h1>
		<LanguageSelector :lang="lang" @update-lang="lang = $event" />
		<CallCounter :goal="goal" :count="callCount" :lang="lang" />
	</header>
	<MusicPlayer />
	<main>
		<ScreeningQuestions
			:questions="questions[lang]"
			:answers="answers[lang]"
			:lang="lang"
			@next-call="nextCall"
		/>
	</main>
</template>

<style>
	.flex {
		display: flex;
	}
	.align-center {
		align-items: center;
	}
	.px-1 {
		padding-inline: 0.5rem;
	}
	.ml-half {
		margin-left: 0.5rem;
	}
	.ml-1 {
		margin-left: 1rem;
	}
	.ml-2 {
		margin-left: 2rem;
	}
	.mr-half {
		margin-right: 0.5rem;
	}
	.mr-1 {
		margin-right: 1rem;
	}
	.mr-2 {
		margin-right: 2rem;
	}
	.mb-1 {
		margin-bottom: 1rem;
	}
	.mb-2 {
		margin-bottom: 2rem;
	}
	.mb-3 {
		margin-bottom: 3rem;
	}
	.gap-1 {
		gap: 0.5rem;
	}
	.lang-selector {
		font-weight: 700;
	}
	.active {
		color: rgb(158, 91, 224);
	}
	.icon {
		font-size: 2rem;
		cursor: pointer;
		transition: all 0.25s ease-in-out;
	}
	.icon:hover {
		color: rebeccapurple;
	}
	.icon:active {
		color: rgb(158, 91, 224);
	}
</style>
