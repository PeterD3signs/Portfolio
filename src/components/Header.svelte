<script lang="ts">
    import "../app.css";
    import { goto } from "$app/navigation";
    import { getStores } from "$app/stores";
    import { type Readable } from "svelte/store";
    import type { Page } from "@sveltejs/kit";
    import { tick } from "svelte";

    const { page }: { page: Readable<Page> } = getStores();
    $: currentPath = $page.url.pathname; // Reactive subscription to the page store

    type Tab = {
        name: string;
        link: string;
        scroll?: boolean;
    };

    // Nav tabs
    export let tabs: Tab[] = [
        { name: "About", link: "/#about", scroll: true },
        { name: "Programming", link: "/programming" },
        { name: "LEGO®", link: "/lego" },
        { name: "Misc", link: "/misc" }
    ];

    // Scroll to the about section if needed
    async function handleClick(tab: Tab): Promise<void> {
        
        const [basePath, hash] = tab.link.split("#");

        if (tab.scroll && hash) {
            if (currentPath !== "/") {
                await goto(`/#${hash}`);
            } else {
                await tick(); // wait for DOM update
                const el = document.getElementById(hash);
                if (el) el.scrollIntoView({ behavior: "smooth" });
            }
        } else {
            await goto(tab.link);
        }

    }

    // Check if current tab is active
    function isActive(link: string): boolean {
        return currentPath === link.split("#")[0];
    }

    function goHome() {
        if (currentPath !== "/") {
            goto("/");
        }
    }

</script>

<header
    class={"z-[10] sticky top-0 px-6 flex items-center justify-between py-4 bg-neutral m-0"}
>
    <!-- name and surname -->
    <button class="font-large text-xl text-primary" on:click={goHome}>
        Piotr <b class="font-bold">Kosowicz</b>
    </button>

    <!-- page buttons without "Get in touch"-->
    <div class="sm:flex items-center gap-4 hidden">
        {#each tabs as tab}
            <a
                href={tab.link}
                on:click|preventDefault={() => handleClick(tab)}
                class={`btn btn btn-soft btn-primary ${ isActive(tab.link) ? "underline" : ""}`}
            >
                <p>{tab.name}</p>
            </a>
        {/each}
        <button class="btn btn-primary" on:click={() => goto('/contact')}>Get in touch</button>
    </div>
</header>
