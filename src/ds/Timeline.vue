<template>
	<div class="timeline">
		<div v-if="title && icon">
			<AnimatedTitle :image="icon"
			:text="title" :active="active" />
		</div>
		<ol class="timeline-list">
			<li v-for="(timeEvent, index) in timeEvents"
			:key="index" @mouseover="active = true"
			@mouseout="active = false">
				<h5>{{ timeEvent.title }}</h5>
				<h6 v-if="timeEvent.duration">
					{{ timeEvent.duration }}
				</h6>
				<p>
					<span v-if="timeEvent.intro" class="intro">
						{{ timeEvent.intro }}
					</span> 
					<span v-html="timeEvent.description"></span>
				</p>
			</li>
		</ol>
	</div>
	
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
	data() {
		return {
			active: false,
		}
	},
	props: {
		timeEvents: {
			type: Array as () => TimeEvent[],
			required: true
		},
		title: {
			type: String,
			required: false
		},
		icon: {
			type: String,
			required: false
		}
	}
})
</script>

<style lang="scss" scoped>
$border: 0.3*$m solid $purple-main;
$bullet-size: 1.3*$m;

.timeline-list {
	list-style: none;
	padding: 0 0 0 2*$m;
	margin: 0 0 0 3*$m;
	border-left: $border;
	z-index: 0;

	li {
		position: relative;
		padding-top: 0.5*$m;

		&:not(:last-child) {
			margin-bottom: 2*$m;
		}

		&:after {
			height: $bullet-size;
			width: $bullet-size;
			display: block;
			position: absolute;
			background: $white;
			border-radius: 50%;
			border: $border;
			content: '';
			top: 0.5*$m;
			left: -3.1*$m;
			z-index: 2;
			transition: all $animation-time ease-in;
			@include animation-on-load(grow-ball);
		}

		&:hover:after {
			background: lighten($purple-main, 10%);
		}

		h5, h6 {
			display: inline-block;
		}

		h5 {
			font-family: 'Bebas Neue';
			font-weight: 600;
			font-size: 2*$m;
		}

		h6 {
			font-family: 'Open Sans';
			font-size: 1*$m;
			margin-left: 0.5*$m;
		}

		p {
			.intro {
				font-weight: 600;
				margin-right: 0.5*$m;
			}

			font-family: 'Open Sans';
			font-size: 1.5*$m;
			text-align: justify;
			line-height: 1.3;
		}
	}
}

@keyframes grow-ball {
	0% {
		transform: scale(0);
	}
}
</style>
