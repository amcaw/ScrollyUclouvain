<script lang="ts">
	// Inspired by:
	// - https://www.linkedin.com/pulse/so-you-want-code-data-story-kontinentalist/
	// - https://www.newline.co/courses/better-data-visualizations-with-svelte
	// - https://github.com/jsonkao/svelte-scrollama

	let {
		flourishID = 3279466,
		steps = ['First step', 'Second step', 'Third step']
	}: { flourishID?: number; steps?: string[] } = $props();

	let activeStepIndex = $state(0);
	let scrollyRef: HTMLElement;

	$effect(() => {
		const observer = new IntersectionObserver(
			(entries) => {
				for (const entry of entries) {
					if (entry.isIntersecting) {
						activeStepIndex = Number((entry.target as HTMLElement).dataset.step);
					}
				}
			},
			{ threshold: 0.5 }
		);

		scrollyRef.querySelectorAll('.step').forEach((el) => observer.observe(el));
		return () => observer.disconnect();
	});
</script>

<section bind:this={scrollyRef} class="section-container">
	<div class="foreground">
		{#each steps as text, index}
			<div class="step" data-step={index}>
				<div class="step-content">
					<p>{@html text}</p>
				</div>
			</div>
		{/each}
	</div>

	<div class="sticky-background">
		<iframe
			src={`https://flo.uri.sh/story/${flourishID}/embed#slide-${activeStepIndex}`}
			title="Interactive or visual content"
			class="flourish-embed"
			frameborder="0"
			scrolling="no"
			style="width:100%;height:100vh;pointer-events:none;"
		></iframe>
	</div>
</section>

<style>
	* {
		box-sizing: border-box;
	}

	.section-container {
		margin-top: 1em;
		text-align: center;
		transition: background 100ms;
		display: flex;
		flex-direction: row;
	}

	.sticky-background {
		position: sticky;
		top: 0;
		height: 100vh;
		flex: 0 1 60%;
		overflow: hidden;
		z-index: 1;
	}

	.foreground {
		display: flex;
		flex-direction: column;
		align-items: center;
		flex: 0 1 40%;
		pointer-events: none;
	}

	.step {
		display: flex;
		justify-content: center;
		align-items: center;
		padding: 20px;
		position: relative;
		z-index: 2;
		width: 100%;
		margin-bottom: 100vh;
	}

	.step:first-child {
		margin-top: 40vh;
	}

	.step:last-child {
		margin-bottom: 0;
		padding-bottom: 100vh;
	}

	.step-content {
		background-color: rgba(245, 245, 245, 0.8);
		box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.2);
		color: black;
		border-radius: 10px;
		padding: 0.5rem 1rem;
		display: flex;
		flex-direction: column;
		justify-content: center;
		z-index: 10;
		font-size: 1rem;
		text-align: left;
		width: 100%;
		max-width: 500px;
		margin: auto;
		pointer-events: auto;
	}

	@media screen and (max-width: 768px) {
		.section-container {
			flex-direction: column-reverse;
		}
		.sticky-background,
		.foreground {
			width: 100%;
		}
		.foreground {
			margin-top: -80vh;
		}
	}
</style>
