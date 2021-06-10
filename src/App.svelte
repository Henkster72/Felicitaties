<script>
	import { onMount } from 'svelte';

	let characters = ['🥳', '🎉', '✨'];

	let confetti = new Array(100).fill()
		.map((_, i) => {
			return {
				character: characters[i % characters.length],
				x: Math.random() * 100,
				y: -20 - Math.random() * 100,
				r: 0.1 + Math.random() * 1
			};
		})
		.sort((a, b) => a.r - b.r);

	onMount(() => {
		let frame;

		function loop() {
			frame = requestAnimationFrame(loop);

			confetti = confetti.map(emoji => {
				emoji.y += 0.7 * emoji.r;
				if (emoji.y > 120) emoji.y = -20;
				return emoji;
			});
		}

		loop();

		return () => cancelAnimationFrame(frame);
	});
</script>

{#each confetti as c}
	<span style="left: {c.x}%; top: {c.y}%; transform: scale({c.r})">{c.character}</span>
{/each}
<h1>
	Gefeliciteerd Sophie!
</h1>
<style>
	:global(body) {
		overflow: hidden;
	}

	span {
		position: absolute;
		font-size: 5vw;
	}
	h1{
		z-index:1000;
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		padding: 5px 20px;
		color: #fff;
		background: linear-gradient(to right, #4d4d4d 0, #fff 10%, #4d4d4d 20%);
		background-position: 0;
		-webkit-background-clip: text;
		-webkit-text-fill-color: transparent;
		animation: shine 3s infinite linear;
		animation-fill-mode: forwards;
		-webkit-text-size-adjust: none;
		font-weight: 600;
		text-decoration: none;
		white-space: nowrap;
		-webkit-text-stroke-width: 1px;
  		-webkit-text-stroke-color: black;
	}
	@-moz-keyframes shine {
	0% {
		background-position: 0;
	}
	100% {
		background-position: 100vw;
	}
	}
	@-webkit-keyframes shine {
	0% {
		background-position: 0;
	}
	100% {
		background-position: 100vw;
	}
	}
	@-o-keyframes shine {
	0% {
		background-position: 0;
	}
	100% {
		background-position: 100vw;
	}
	}
	@keyframes shine {
	0% {
		background-position: 0;
	}
	100% {
		background-position: 100vw;
	}
	}
/* Small devices (tablets, 768px and up) */

@media screen and (max-width: 600px)  {
    h1 {
        font-size: 2em;
    }
}

/* Medium devices (desktops, 992px and up) */
@media screen and (min-width: 800px) {
    h1 {
        font-size: 5em;
    }
}

/* Large devices (large desktops, 1200px and up) */
@media screen and (min-width: 1200px) {
    h1 {
        font-size: 7em;
    }
}
</style>