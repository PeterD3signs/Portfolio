<script lang="ts">
    import Header from "../components/Header.svelte";
	import '../app.css';
	import Footer from "../components/Footer.svelte";

    function goTop() {
        document.body.scrollIntoView();
    }

	let { children } = $props();
</script>
<Header />
<div
    class="container relative flex flex-col max-w-[1400px] mx-auto w-full text-sm sm:text-base min-h-screen"
>
    {@render children()}
</div>
<Footer />
