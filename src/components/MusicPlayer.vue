<template>
	<button @click="isPlaying ? pausePlayer() : resumePlayer()">
		{{ isPlaying ? "Pause" : "Play" }}
	</button>
</template>

<script>
	export default {
		name: "MusicPlayer",
		props: {
			url: {
				type: String,
				// required: true,
				default: "https://dl.espressif.com/dl/audio/ff-16b-2c-44100hz.m4a",
			},
			autoPlay: {
				type: Boolean,
				default: false,
			},
		},
		data() {
			return {
				player: new Audio(),
				isPlaying: false,
				song: new URL("/src/assets/audio/eng/engQ1.m4a", import.meta.url),
			};
		},
		mounted() {
			console.log(this.song);
			this.player.src = this.song;
		},
		methods: {
			resumePlayer() {
				this.player.play();
				this.isPlaying = true;
			},
			pausePlayer() {
				this.player.pause();
				this.isPlaying = false;
			},
		},
	};
</script>

<style scoped>
	button {
		border: rebeccapurple 2px solid;
		border-radius: 15px;
		padding: 0.25rem 0.5rem;
		margin-bottom: 1rem;
	}
</style>
