<template>
	<div>{{ lang === "esp" ? "Meta de hoy: " : `Today's goal: ` }}{{ goal }}</div>
	<div v-if="lang === 'esp'" class="flex align-center">
		<span class="mr-half">
			<input type="number" name="count" id="count" v-model="_count" />
			Llevas <label for="count">{{ count }}</label> llamadas.</span
		>
		<span v-if="remaining < 0">Bien!! la milla extra.</span>
		<span v-else-if="remaining <= 50"
			>Casi terminas, solo faltan:
			<span :style="{ color: `rgba(158, 91, 224, ${alphaMissingCalls})` }">{{
				remaining
			}}</span>
		</span>
		<span v-else-if="remaining <= 100" class="flex align-center"
			>Vas bien! Ya casi terminas.
			<Icon icon="fa6-solid:face-smile-wink" class="ml-half"
		/></span>
		<span v-else-if="remaining <= 150" class="flex align-center"
			>Animos, ya vas por la mitad o cerca.
			<Icon class="ml-half" icon="fa6-solid:face-smile-beam"
		/></span>
		<span v-else-if="remaining <= 200" class="flex align-center">
			<Icon class="ml-half" icon="fa6-solid:face-grin-squint"
		/></span>
	</div>
	<div v-else class="flex align-center">
		<span class="mr-half">
			<input type="number" name="count" id="count" v-model="_count" />
			You have <label for="count" editable>{{ count }}</label> calls.</span
		>
		<span v-if="remaining < 0">The extra mile right?</span>
		<span v-else-if="remaining <= goal / 3.75">
			Wrapping up, just missing at least:
			<span :style="{ color: `rgba(158, 91, 224, ${alphaMissingCalls})` }">{{
				remaining
			}}</span>
		</span>
		<span v-else-if="remaining <= goal / 2.75" class="flex align-center"
			>You're doing good! Almost done.
			<Icon class="ml-half" icon="fa6-solid:face-smile-wink"
		/></span>
		<span v-else-if="remaining <= goal / 1.75" class="flex align-center"
			>Cheers, you are near the middle.
			<Icon class="ml-half" icon="fa6-solid:face-smile-beam"
		/></span>
		<span v-else-if="remaining <= goal / 1.25" class="flex align-center"
			>Niceee, getting some progress.
			<Icon class="ml-half" icon="fa6-solid:face-grin-squint"
		/></span>
	</div>
</template>

<script>
import { Icon } from "@iconify/vue";
export default {
	name: "CallCounter",
	emits: ["update-count"],
	components: {
		Icon,
	},
	props: {
		goal: {
			type: [String, Number],
			default: 0,
		},
		count: {
			type: [Number, String],
			default: 0,
		},
		lang: String,
	},
	computed: {
		alphaMissingCalls() {
			return this.count / this.goal;
		},
		_count: {
			get() {
				return this.count;
			},
			set(val) {
				if (new RegExp("[0-9]$").test(Number(val)))
					this.$emit("update-count", Number(val));
			},
		},
		remaining() {
			return this.goal - this.count;
		},
	},
};
</script>

<style scoped>
#count {
	opacity: 0;
	float: right;
	border: none;
	outline: none;
	display: flex;
	width: 40px;
}
#count:focus + label {
	border-bottom: 2px solid gray;
	padding: 0 0.25rem;
	transition: all 0.2s ease-in-out;
	position: relative;
}
#count:focus + label::before {
	width: 1px;
	height: 80%;
	background: #333;
	position: absolute;
	top: 50%;
	right: 0;
	content: "";
	transform: translate(-50%, -50%);
	animation: blink 0.95s ease-in-out infinite;
	opacity: 1;
}
@keyframes blink {
	to {
		opacity: 0;
	}
}
</style>
