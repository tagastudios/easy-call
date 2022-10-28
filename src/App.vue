<script setup>
import LanguageSelector from "./components/LanguageSelector.vue";
import ScreeningQuestions from "./components/ScreeningQuestions.vue";
import CallCounter from "./components/CallCounter.vue";
// import { PrismaClient } from "@prisma/client";
import { ref } from "vue";

const lang = ref("eng");
const callCount = ref(0);
const goal = 200;

// const prisma = new PrismaClient();

const questions = {
	esp: {
		text: [
			"Estaba haciendo una encuesta a ver si me ayuda?",
			"Cual es su principal preocupacion",
			"Yadira Caraveo",
			"Jena Griswald",
		],
		audio: [
			"/src/assets/audio/esp/espQ1.m4a",
			"/src/assets/audio/esp/espQ2.m4a",
			"/src/assets/audio/esp/espQ3.m4a",
			"/src/assets/audio/esp/espQ4.m4a",
			"/src/assets/audio/esp/espQ5.m4a",
		],
	},
	eng: {
		text: [
			`I'm doing a short survey, can you help?`,
			`What's the main concern?`,
			"Yadira Caraveo",
			"Jena Griswald",
		],
		audio: [
			"/src/assets/audio/eng/engQ1.m4a",
			"/src/assets/audio/eng/engQ2.m4a",
			"/src/assets/audio/eng/engQ3.m4a",
			"/src/assets/audio/eng/engQ4.m4a",
			"/src/assets/audio/eng/engQ5.m4a",
		],
	},
};

const answers = {
	esp: {
		"Ok perfecto, muchas gracias": "/src/assets/audio/esp/espA1.m4a",
		"Oh! Disculpe la molestia": "/src/assets/audio/esp/espA2.m4a",
		"Muchas gracias y bonito dia": "/src/assets/audio/esp/espAfinal.m4a",
	},
	eng: {
		"Alright, thank you!": "/src/assets/audio/eng/engA1.m4a",
		"Oh, I'm sorry": "/src/assets/audio/eng/engA2.m4a",
		"Perfect, thanks and good day": "/src/assets/audio/eng/engAfinalDay.m4a",
		"Perfect, thanks and good night":
			"/src/assets/audio/eng/engAfinalNight.m4a",
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
	color: var(--primary-color);
}
.icon {
	font-size: 2rem;
	cursor: pointer;
	transition: all 0.25s ease-in-out;
	color: var(--primary-color);
	/* filter: drop-shadow(0px 0 2px var(--secondary-color)); */
	box-shadow: 0px 0px 0px 2px var(--secondary-color);
	border-radius: 50px;
	padding: 1px;
}
.icon:hover {
	color: var(--secondary-color);
}
.icon:active,
.icon-active {
	padding: 0px;
	color: var(--primary-color);
}
.icon-active {
	color: var(--secondary-color);
}
.icon-active:hover {
	padding: 1px;
}
</style>
