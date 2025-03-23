<script lang="ts">
	import background from "$lib/assets/background-dark-green.png";
	import demo from "$lib/assets/demo-small-screen.png";
    import { onDestroy, onMount } from "svelte";
    import {  blur, slide } from "svelte/transition";
    import Tooltip from "sv-tooltip"

    let greetings = ['Terminal', 'SSH', 'Command Prompt', 'Shell', 'Console', 'Bash', 'Command Line', 'PowerShell'];

    let index = $state(0);
	let roller: number;

    let tooltip = $state("Copy");

    let ssh_command = "ssh pomo.sairashgautam.com.np"
	
	onMount(() => {
		roller = setInterval(() => {
			if (index === greetings.length - 1) index = 0;
			else index++;
		}, 2000);
	});

    function clickCopyToClipboard() {
        tooltip = "Copied";
        navigator.clipboard.writeText(ssh_command);
        setTimeout(() => {
            tooltip = "Copy"
        }, 1000);
    }


    onDestroy(() => {
		clearInterval(roller);
	});
</script>

<div class="relative px-4">

    <section
        id="homepage-hero"
        class="border-b border-b-border-light pb-5 pt-12 md:pb-12 md:pt-[120px] "
        
    >
        <section id=":S1:" class="relative-z-5">
            <div class="new-container z-10 ">
                <div
                    class="relative border border-border-light bg-black px-5 py-[72px]"
                >
                    <img
                        alt="Top Backgrond"
                        draggable="false"
                        fetchpriority="high"
                        width="2112"
                        height="816"
                        decoding="async"
                        data-nimg="1"
                        class="pointer-events-none absolute inset-0 left-px m-auto h-full w-full select-none object-cover opacity-80"
                        src={background}
                        style=""
                    />
                    <div class="py-2 text-center">
                        <div class="text-5xl font-bold tracking-normal">Total Zen</div>
                        <div class="mt-3 h-10">
                            {#key index}
                                <div class="" transition:blur>
                                    <div class="text-3xl font-bold text-[#bfedc1]"  transition:slide>{greetings[index]}</div>
                                </div>
                            {/key}
                        </div>
                        <div class="mt-4 text-xl font-semibold">
                            Pomodoro
                        </div>

                        <div class="flex justify-center">
                            <div class="mt-4 py-2 px-4 bg-gray-800 max-w-xs text-left rounded-l">
                                {ssh_command}
                            </div>
                            <div class="mt-4 bg-white text-black text-left rounded-r" >
                                <Tooltip tip={tooltip} color="white" top>
                                    <button class="pt-2 px-4 cursor-pointer" aria-label="Copy To Clipboard" onclick={()=>{clickCopyToClipboard()}}>
                                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="size-6">
                                            <path fill-rule="evenodd" d="M10.5 3A1.501 1.501 0 0 0 9 4.5h6A1.5 1.5 0 0 0 13.5 3h-3Zm-2.693.178A3 3 0 0 1 10.5 1.5h3a3 3 0 0 1 2.694 1.678c.497.042.992.092 1.486.15 1.497.173 2.57 1.46 2.57 2.929V19.5a3 3 0 0 1-3 3H6.75a3 3 0 0 1-3-3V6.257c0-1.47 1.073-2.756 2.57-2.93.493-.057.989-.107 1.487-.15Z" clip-rule="evenodd" />
                                        </svg>
                                    </button>
                                </Tooltip>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>
        <div class="new-container relative-z-5">
            <div class="z-10 relative">
                <img
                    alt="demo"
                    fetchpriority="high"
                    width="4026"
                    height="2379"
                    decoding="async"
                    data-nimg="1"
                    class="border-x border-b border-border-light bg-black"
                    src={demo}
                />
            </div>
        </div>
        
    </section>
</div>
