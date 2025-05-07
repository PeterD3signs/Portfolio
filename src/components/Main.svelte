<script lang="ts">
	import '../app.css';
	import AnimatedRectangles from './AnimatedRectangles.svelte';
	import Carousel from './Carousel.svelte';
    import Terminal from './Terminal.svelte';

	let ProgCardArr = [
		{
			img_src: 'favicon.png',
			img_alt: 'Placeholder image',
			title: 'Prog 1',
			text: 'Description of project 1'
		},
		{
			img_src: 'favicon.png',
			img_alt: 'Placeholder image',
			title: 'Prog 2',
			text: 'Description of project 2'
		},
		{
			img_src: 'favicon.png',
			img_alt: 'Placeholder image',
			title: 'Prog 3',
			text: 'Description of project 3'
		},
		{
			img_src: 'favicon.png',
			img_alt: 'Placeholder image',
			title: 'Prog 4',
			text: 'Description of project 4'
		}
	];
	let LegoCardArr = [
		{
			img_src: 'favicon.png',
			img_alt: 'Placeholder image',
			title: 'l 1',
			text: 'Description of project 1'
		},
		{
			img_src: 'favicon.png',
			img_alt: 'Placeholder image',
			title: 'l 2',
			text: 'Description of project 2'
		},
		{
			img_src: 'favicon.png',
			img_alt: 'Placeholder image',
			title: 'l 3',
			text: 'Description of project 3'
		},
		{
			img_src: 'favicon.png',
			img_alt: 'Placeholder image',
			title: 'l 4',
			text: 'Description of project 4'
		}
	];
</script>

<main class="flex flex-1 flex-col p-4">
	<AnimatedRectangles rectSize={60} baseColor={[255, 99, 132]} />
	<section id="introPage" class="grid grid-cols-1 gap-10 py-8 sm:py-14 lg:grid-cols-2">
		<div class="flex flex-col gap-6 text-center md:gap-2 lg:justify-center lg:gap-4 lg:text-left">
			<h2 class="text-5xl font-semibold sm:text-5xl md:text-5xl">
				<br /> <span class="poppins text-primary">Hello world!</span>
			</h2>
			<h2 class="text-5xl font-semibold sm:text-5xl md:text-5xl">
				My name is <span class="poppins text-primary">Piotr Kosowicz</span>,
				<br /> I am an:
			</h2>
			<div
				class="flex flex-col gap-6 text-center md:gap-2 lg:justify-center lg:gap-10 lg:text-left"
			>
				<h2 class="text-5xl font-semibold sm:text-5xl md:text-5xl">
					- <span class="poppins text-primary">IT Student</span>
					<br />- <span class="poppins text-primary">Custom set designer</span>
					<br />- <span class="poppins text-primary">Ambitious learner</span>
				</h2>
				<p class="text-base sm:text-lg md:text-xl">
					I constantly look for <span class="poppins text-primary">new challanges</span>,
					<span class="poppins text-primary">interesting projects</span>
					and <span class="poppins text-primary">opportunities to expad my knowledge</span>. What
					brings me the most joy, is
					<u
						>elevating things from good enough, to <span class="poppins text-primary"
							>as good as possible</span
						></u
					>.
				</p>
			</div>
		</div>
		<div class="relative grid place-items-center shadow-2xl">
			<img src={'favicon.png'} alt="-" class="z-[2] max-h-[70vh] object-cover" />
		</div>
	</section>
	<section id="about" class="w-full space-y-4">
		<div class="flex w-full justify-between">
			<h2 class="text-5xl font-semibold sm:text-5xl md:text-5xl">
				↙ Some of my <span class="poppins text-primary">Programming projects</span>
			</h2>
		</div>
        <p> some placeholder text </p>
		<Carousel cards={ProgCardArr} moveRight={true} />
		<div class="flex w-full justify-end">
			<Terminal />
		</div>
		<div class="flex w-full justify-end">
			<h2 class="text-5xl font-semibold sm:text-5xl md:text-5xl">
				Some of my <span class="poppins text-primary">LEGO projects</span> ↘
			</h2>
		</div>
		<div>
			<p>click <a href="/programming">here</a> for details...</p>
		</div>
		<Carousel cards={LegoCardArr} />
	</section>
</main>
