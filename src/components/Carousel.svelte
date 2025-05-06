<script lang="ts">
    import { onMount } from "svelte";
	export let cards: Array<{
		title: string;
		text: string;
		img_src: string;
		img_alt: string;
	}>;
    export let moveRight: boolean = false; // Set to true to turn the carousel right

	let pause = false;
    let cardList: HTMLUListElement;

    onMount(() => {     //appending visual clones of the elements to the end of the list
        if (cardList.getAttribute('data-cloned') === 'true') return;    //adding this check to avouid cloning the element multiple times when dynamically hiding and showing the carousel
        cardList.setAttribute('data-cloned', 'true');

        const children = Array.from(cardList.children);
        children.forEach((child) => {
            const clone = child.cloneNode(true) as HTMLElement;
            clone.setAttribute('aria-hidden', 'true');
            cardList.appendChild(clone);
        });
    });

</script>

<div 
    class="MyCarousel"
    aria-label="Pause auto-scroll on hover"
    role="region"
    on:mouseover={() => (pause = true)}
	on:mouseout={() => (pause = false)}
	on:focus={() => (pause = true)}
	on:blur={() => (pause = false)}
>
	<ul
		class="Carousel-List"
		style="animation-play-state: {pause ? 'paused' : 'running'}; animation-direction: {moveRight ? 'reverse' : 'forwards'};"
        
        bind:this={cardList}
	>
		{#each cards as card}
			<li>
				<div class="card bg-base-100 w-96 shadow-sm">
					<figure>
						<img src={card.img_src} alt={card.img_alt} />
					</figure>
					<div class="card-body">
						<h2 class="card-title">{card.title}</h2>
						<p>
							{card.text}
						</p>
					</div>
				</div>
			</li>
		{/each}
	</ul>
</div>

<style lang="css">

    /*
    DaisyUI does not come with a good auto-scroll carousel, so I opted to make my own with pure CSS.
    I still used some classes from DaisyUI like 'card' or 'button', so this file is a hybrid solution.
    */

	.MyCarousel {
        flex-wrap: nowrap;
		overflow: hidden;
		mask: linear-gradient(to right, transparent, white 20%, white 80%, transparent);
	}

	.Carousel-List {
		width: max-content;
		flex-wrap: nowrap;
		padding-block: 1rem;
		display: flex;
		gap: 1rem;
		animation: scroll 30s linear infinite;
	}

	@keyframes scroll {
		to {
			transform: translate(calc(-50% - 0.5rem));
		}
	}

</style>
