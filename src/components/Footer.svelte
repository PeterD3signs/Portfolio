<script lang="ts">
	import FacebookIcon from "./icons/facebook_icon.svelte";
    import InstagramIcon from "./icons/instagram_icon.svelte";
    import LinkedInIcon from "./icons/linkedin_icon.svelte";
    import YoutubeIcon from "./icons/youtube_icon.svelte";
    import GithubIcon from "./icons/github_icon.svelte";
    import MailIcon from "./icons/mail_icon.svelte";
    import LegoIcon from "./icons/lego_icon.svelte";
	import type { SvelteComponent } from "svelte";

    interface LinkItem {
        name: string;
        url: string;
        icon: SvelteComponent;
        color?: string;
}

    const socialLinks = [
        {
			name: 'mail',
			url: 'mailto:kosowicz.peter+programming@gmail.com?subject=Hey, I have just seen your portfolio and wanted to ask some questions :)',
			icon: MailIcon
		},
		{
			name: 'LinkedIn',
			url: 'https://www.linkedin.com/in/piotr-kosowicz-4896b9352',
			icon: LinkedInIcon
		},
		{
			name: 'GitHub',
			url: 'https://github.com/PeterD3signs',
			icon: GithubIcon
		},
		{
			name: 'Youtube',
			url: 'https://www.youtube.com/watch?v=dQw4w9WgXcQ',
			icon: YoutubeIcon
		}
	];

	const legoLinks = [
        {
			name: 'mail',
			url: 'mailto:designmyownset@gmail.com?subject=Hey, I have some questions regarding your LEGO® projects ;)',
			icon: MailIcon
		},
		{
			name: 'LEGO® Ideas',
			url: 'https://ideas.lego.com/profile/peter_designs',
			icon: LegoIcon
		},
		{
			name: 'Instagram',
			url: 'https://www.instagram.com/design.my.own.set',
			icon: InstagramIcon
		},
		{
			name: 'Facebook',
			url: 'https://www.facebook.com/design.my.new.set',
			icon: FacebookIcon
		}
	];
</script>

<footer class="bg-base-200 text-base-content mt-10 p-6">
	<div>
        <h2 class="m-0 text-2xl font-bold">Socials</h2>
    </div>
    <div class="mx-auto flex max-w-screen-xl flex-col items-end justify-between gap-6 sm:flex-row sm:items-start sm:justify-end">

		<div class="flex flex-col gap-10 sm:flex-row">
			<!-- Main Section -->
			<div>
				<h3 class="text-xl mb-2 font-semibold">Main</h3>
				{#each socialLinks as link}
					<a
						href={link.url}
						target="_blank"
						rel="noopener"
						class="mb-1 flex items-center gap-2 hover:underline"
					>
                        <svelte:component this={link.icon} class = 'text-primary'/>
						<span>{link.name}</span>
					</a>
				{/each}
			</div>

			<!-- LEGO Section -->
			<div>
				<h3 class="text-xl mb-2 font-semibold">LEGO®</h3>
				{#each legoLinks as link}
					<a
						href={link.url}
						target="_blank"
						rel="noopener"
						class="mb-1 flex items-center gap-2 hover:underline"
					>
                        <svelte:component this={link.icon} class = 'text-primary'/>
						<span>{link.name}</span>
					</a>
				{/each}
			</div>

		</div>
	</div>
</footer>
