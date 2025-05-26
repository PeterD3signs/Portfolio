<script lang="ts">
    import { tick } from 'svelte';

    let inputField: HTMLInputElement;

	let command = '';
	let output: string[] = [];
	let terminalLocked = true;
	let showPrompt = false;
	let terminalVisible = false;
	let currentLine = '';
    let now = new Date();
    let nowStr = now.toLocaleString('en-US', {
        month: 'short',
        day: 'numeric',
        hour: '2-digit',
        minute: '2-digit'
    });

	const scriptedCommands = [
        { type: 'command', text: 'pwd' },
        { type: 'response', text: 'Piotrs-Website/about' },
		{ type: 'command', text: 'ls -al' },
        { type: 'response', text: 'total 50' },
		{ type: 'response', text: 'drwxrwxr-x  5 admin   staff  320 ' + nowStr + ' LEGO' },
		{ type: 'response', text: 'dr-xr-xr-x  2 admin   staff  112 ' + nowStr + ' secret' },
		{ type: 'response', text: 'drwxr-xr-x  5 admin   staff  544 ' + nowStr + ' contact' },
		{ type: 'command', text: 'mkdir programming' },
		{ type: 'command', text: 'echo "write \'cd programming\' and press ENTER to learn more about my projects and skills :)"'},
		{ type: 'response', text: 'write "cd programming" to learn more about my projects and skills :)'}
	];

	let typingSpeed = 100;

	async function typeCommand(text: string) {
		currentLine = 'user@website:~$ █';
		for (let i = 0; i < text.length; i++) {
			currentLine = currentLine.slice(0, -1) + text[i] + '█';
			await new Promise((r) => setTimeout(r, typingSpeed));
		}
		output = [...output, currentLine.slice(0, -1)];
		currentLine = '';
	}

	async function runScript() {
		for (const entry of scriptedCommands) {
			if (entry.type === 'command') {
                if (entry.text ===  'mkdir programming'){
                    typingSpeed = 60;
                }
                if (entry.text ===  'echo "write \'cd programming\' and press ENTER to learn more about my projects and skills :)"'){
                    typingSpeed = 30;
                }
				await typeCommand(entry.text);
			} else {
				output = [...output, entry.text];
			}
		}
		showPrompt = true;
		terminalLocked = false;
        await tick(); // Wait for DOM update
        inputField.focus(); // Focus the input field after typing
	}

	function handleCommand(event: KeyboardEvent) {
		if (event.key === 'Enter' && !terminalLocked) {

			const cmd = command.trim();
			
            switch (cmd) {
                case "cd banana":
                    window.location.href = '/secret';
                    break;
                case "cd contact":
                    window.location.href = '/contact';
                    break;
                case "cd programming":
                    window.location.href = '/programming';
                    break;
                case "cd LEGO":
                case "cd Lego":
                case "cd lego":
                    window.location.href = '/lego';
                    break;
                default:
                    output = [...output, 'user@website:~$ ' + command, 'Error 404: Unknown command / Too high expectations ;)'];
            }

			command = '';
            inputField.focus(); // Refocus the input field after command execution
		}
	}

	function toggleTerminal() {
		terminalVisible = true;
		setTimeout(runScript, 300); // slight delay to allow transition
	}
</script>

<div class="w-full max-w-full font-mono">
	<!-- Title Bar / Launcher -->
	{#if !terminalVisible}
		<div
			role="button"
			tabindex="0"
			aria-label="Open terminal"
			class="cursor-pointer rounded-md bg-gray-800 py-2 text-center shadow-md"
			on:click={toggleTerminal}
			on:keydown={(e) => e.key === 'Enter' && toggleTerminal()}
		>
			<p class="text-primary"><u>Click here to learn more about my Projects and Skills!</u></p>
		</div>
	{/if}

	{#if terminalVisible}
		<div class="h-screen w-full overflow-hidden bg-black rounded-md border border-gray-700 shadow-md">
			<!-- Title Bar -->
			<div class="bg-gray-800 px-4 py-2 text-sm font-semibold text-gray-300">
				<p class="text-primary">Terminal</p>
			</div>

			<!-- Terminal Body -->
			<div class="h-[calc(100vh-3.5rem)] space-y-2 overflow-y-auto bg-black p-4">
				{#each output as line}
					<div><p>{line}</p></div>
				{/each}

				{#if currentLine}
					<div><p>{currentLine}</p></div>
				{/if}

				{#if showPrompt}
					<div class="flex">
						<span class="mr-2">user@website:~$ </span>
						<input
							bind:value={command}
							on:keydown={handleCommand}
							class="w-full bg-transparent outline-none"
							autocomplete="off"
							autocorrect="off"
							spellcheck="false"
                            bind:this={inputField}
						/>
					</div>
				{/if}
			</div>
		</div>
	{/if}
</div>

<style>
	input::placeholder {
		color: #6b6b6b;
	}
</style>
