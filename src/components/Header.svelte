<script lang="ts">
    import "../app.css";

    export let tabs = [
        { name: "About", link: "#about" },    
        { name: "Programming", link: "#programming" },
        { name: "LEGO®", link: "#lego" },
        { name: "Misc", link: "#misc" },
];
</script>

<header
    class={" z-[10] sticky top-0 px-6 flex items-center justify-between py-4 bg-neutral m-0"}
>
    <h1 class="font-large text-xl text-primary">
        Piotr <b class="font-bold">Kosowicz</b> <span class="">
        </span>
    </h1>
    <div class="sm:flex items-center gap-4 hidden">
        {#each tabs as tab, index}
            <a
                href={tab.link}
                class="btn btn-soft btn-primary"
                target={index === 2 ? "_blank" : ""}
            >
                <p>{tab.name}</p>
            </a>
        {/each}
        <button class="btn btn-primary">Get in touch</button>
    </div>
</header>