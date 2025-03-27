<script lang="ts">
	import background from "$lib/assets/background-dark-green.png";
	import demo from "$lib/assets/demo-small-screen.png";
    import { onDestroy, onMount } from "svelte";
    import { Popover} from 'flowbite-svelte';
    import {  blur, slide } from "svelte/transition";
    import Tooltip from "sv-tooltip"

    import RightIcon from "$lib/icons/right.svelte";
    import DownIcon from "$lib/icons/down.svelte";

    import BadgeCheck from "$lib/icons/badge-check.svelte";
    import sshpomosairashgautamcomnp from "$lib/assets/sshpomosairashgautamcomnp.png"
    import step2 from "$lib/assets/step2.png"
    import step3 from "$lib/assets/step3.png"
    import tree_png from "$lib/assets/tree.gif"
    import flowgif from "$lib/assets/flow.gif"
    import flow from "$lib/assets/flow.png"
    import coffee from "$lib/assets/coffee.gif"

    let greetings = ['Terminal', 'SSH', 'Command Prompt', 'Shell', 'Console', 'Bash', 'Command Line', 'PowerShell'];

    let tree = `
                 ######
              ### |######
              #\\/\\  \\/ //##
             #    | /| / \\/#
            #\\  |        / ##
            #\\ \\\\  /  /    /#
            #    \\\\|  | / //#
                   |  //
                   \\ / 
                    \\/

                    /  
                    |
                    |
########################################`

    let index = $state(0);
	let roller: number;

    let tooltip = $state("Copy");

    let downInterval: number
    let isBlogHovered = $state(true)
    let downIconHover = $state(false)

    let ssh_command = "ssh pomo.sairashgautam.com.np"



    let scrollPercent = $state(0);
    let targetDiv: HTMLElement;

    const calculateScrollPercentage = (element: HTMLElement) => {
        const rect = element.getBoundingClientRect();
        const elementTop = rect.top + window.scrollY;
        const elementBottom = rect.bottom + window.scrollY;
        const viewportHeight = window.innerHeight;

        const start = elementTop - viewportHeight;
        const end = elementBottom;
        const currentScroll = window.scrollY;

        if (end === start) {
        return currentScroll >= elementTop ? 100 : 0;
        }

        let percentage = ((currentScroll - start) / (end - start)) * 100;
        return Math.min(100, Math.max(0, percentage));
    };
	
	onMount(() => {
		roller = setInterval(() => {
			if (index === greetings.length - 1) index = 0;
			else index++;
		}, 2000);

        downInterval = setInterval(()=>{
            if(scrollPercent < 68) {
                downIconHover = true

                setTimeout(() => {
                    downIconHover = false;
                }, 200);
            }
        }, 1000)


        const handleScroll = () => {
        if (!targetDiv) return;
        scrollPercent = calculateScrollPercentage(targetDiv);
        };

        window.addEventListener('scroll', handleScroll);
        handleScroll(); // Initial calculation

        return () => window.removeEventListener('scroll', handleScroll);
	});

    function clickCopyToClipboard() {
        tooltip = "Copied";
        navigator.clipboard.writeText(ssh_command);
        setTimeout(() => {
            tooltip = "Copy"
        }, 1000);

        
    }


    function handleBlogMouseEnter() {
		isBlogHovered = true;

		setTimeout(() => {
			isBlogHovered = false;
		}, 200);
	}

    function showLinesFromBottom(text: string, percent:number): string[] {
        percent = Math.max(10, Math.min(68, percent));
        const lines = text.split('\n');
        const totalLines = lines.length;

        const linesToShow = Math.max(1, Math.round(((percent - 10) / 58) * (totalLines - 1)) + 1);;

        
        return [...Array(5 +totalLines - linesToShow).fill(""), ...lines.slice(totalLines - linesToShow)];
    }
    


    onDestroy(() => {
		clearInterval(roller);
		clearInterval(downInterval);
	});


    
</script>

<div class="my-16 mb-12 flex justify-center text-sm">
    <a href="https://sairash.hashnode.dev/how-to-host-a-ssh-app-using-nginx" class="bg-[#CFF27E] text-black pl-4 pr-2 py-1 shadow-md shadow-[#bfedc1] rounded block max-w-[350px] text-center"  onmouseenter={handleBlogMouseEnter}>
        <span class="flex justify-center text-[#000] gap-1">
            <BadgeCheck isHovered={true} size={20} classes="mt-0.5" />
            <span class="mt-1 -mr-1"><b>Blog: </b> Host Your Own Ssh App </span>
            <RightIcon isHovered={isBlogHovered} size={24} />
        </span>
    </a>
</div>
<div class="relative px-4">

    <section
        id="homepage-hero"
        class="border-b border-b-border-light pb-5 pt-12 md:pb-12  "
        
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

                        <div class="flex justify-center mt-4">
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

                        <div class="mt-5 text-sm font-semibold text-[#CFF27E]">
                            <a href="/#install-local" class="border-b-2">or run it locally</a>
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

        <section class="mt-24 mb-16 text-center flex justify-center">
            <div class="max-w-lg">
                <div class="mb-2  text-[#CFF27E]">Focus</div>
                <div class="text-3xl font-bold text-[#49beaa]">What is Pomodoro?</div>
                <!-- <div class="mt-3">A visually appealing and distraction free pomodoro experience right within your terminal.</div> -->
                <div class="mt-3">A method for staying focused and mentally fresh.</div>
            </div>
        </section>

        <section id=":S2:" class="relative-z-5">
            <div class="new-container z-10 ">
                <div
                    class="border border-border-light bg-black py-8"
                >
                    <div class="px-5 py-2">
                        It is a popular time management method which asks you to alternate pomodoros — focused work sessions — with frequent short breaks to promote sustained concentration and stave off mental fatigue.
                    
                        <div class="my-6">
                            <div class="mb-2 text-[#bfedc1] font-bold">Timeline:</div>
                            <ol class="pl-4">
                                <li>✏️ Pick a task</li>
                                <li>⏳ Set a 25 minute timer</li>
                                <li>🧑🏽‍💻 Work on your task until the task is done.</li>
                                <li>☕ Take a 5 min break</li>
                                <li>🌲 Every 4 pomodors, take a longer 15-30 minute break</li>
                            </ol>
                        </div>

                        <div class="mb-4">
                            <div class=" text-[#bfedc1] font-bold">
                                We love this method because it:
                            </div>

                            <ol class="mt-2 mb-5  pl-4">
                                <li>👀 Improves focus</li>
                                <li>🧿 Minimizes distractions</li>
                                <li>🪫 Prevents burnout</li>
                                <li>🥸 Promotes accountability</li>
                                <li>💪🏽 Boosts motivation</li>
                            </ol>
                            <div class="">
                                <div class=" text-[#bfedc1] font-bold">
                                    Learn more:
                                </div>
    
                                
                                <div class="pl-4 mt-2">
                                    - <a class="border-b-2 text-[#CFF27E]" target="_blank" href="https://www.forbes.com/sites/bryancollinseurope/2020/03/03/the-pomodoro-technique/">Forbs: The Pomodoro Technique Explained </a> <br>
                                    - <a class="border-b-2 text-[#CFF27E]" target="_blank" href="https://www.youtube.com/watch?v=mNBmG24djoY">Youtube: POMODORO TECHNIQUE - My Favorite Tool .. </a>
                                </div>
                            </div>
                        </div>
                    </div>
                   
                </div>
            </div>
        </section>


        <section class="mt-24 mb-16 text-center flex justify-center">
            <div class="max-w-lg">
                <div class="mb-2  text-[#CFF27E]">Convenient</div>
                <div class="text-3xl font-bold text-[#49beaa]">What is Pomossh?</div>
                <div class="mt-3">A visually appealing and distraction free pomodoro experience right within your terminal.</div>
            </div>
        </section>



        <section id="maincontent" bind:this={targetDiv} class="relative-z-5">
            <div class="new-container z-10 ">
                <div
                    class=" border border-border-light bg-black relative flex sm:flex-row-reverse"
                >
                    <div class="pt-2 hidden sm:block">
                        <div class="text-sm sticky top-20 sm:text-[10px] md:text-[14px] lg:text-[16px] mt-10  sm:right-2 p-2 bg-black sm:inline-block w-full sm:w-auto flex justify-center">
                            <div id="first_tree" class="sm:inline-block text-[#765200] font-bold">
                                <div class="font-bold neon">
                                    {#each showLinesFromBottom(tree, scrollPercent) as v, i }
                                    <span>
                                        {#each v as every }
                                            <pre class={["inline" , (every == "#" && i != showLinesFromBottom(tree, scrollPercent).length - 1)?"text-[#65976f] neon-green":""]} >{every}</pre >
                                        {/each}
                                        <br>
                                    </span>
                                    {/each}
                                </div>
                                <div class="text-center mt-2 font-bold flex justify-center gap-1">
                                    <div class="py-1">Scroll</div>
                                    <DownIcon isHovered={downIconHover} size={24} />
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="w-full px-5 pt-10 pb-[72px]  border-r-2 border-border-light ">
                        <p class="intro">
                            Introducing a fresh take on productivity, a unique Pomodoro Timer app designed specifically for the terminal enthusiasts and tech-savvy professionals. 
                            <span class="my-2 block">
                                This minimalist design keeps your focus on tasks without the clutter of traditional apps. 
                            </span>
                                Furthermore, the app offers the ability to SSH into it using a command <span class="text-[#CFF27E] bg-zinc-800 rounded px-2 py-1 inline-block">ssh pomo.sairashgautam.com.np</span>, allowing you to manage your sessions remotely, whether you're on your local machine or from a server. 
                                <br>
                                <br>
                                Let's see how to use pomossh:
                        </p>
                        <div class="sm:ml-4 mt-5">
                            <div class="">
                                <div class="font-bold text-[#bfedc1]">Step [1]:</div>
                                <div class="mt-3 sm:pl-4">
                                    Run the following comamnd in your terminal 
                                    <img src={sshpomosairashgautamcomnp} class="w-full" alt="">
                                    or install it locally.
                                </div>

                            </div>

                            <div class="mt-10">
                                <div class="font-bold text-[#bfedc1]">Step [2]: </div>
                                <div class="mt-3 sm:pl-4">
                                    Enter the time in minutes and also session "Title"
                                    <img src={step2} class="w-full" alt="">
                                </div>

                            </div>

                            <div class="">
                                <div class="font-bold text-[#bfedc1]">Step [3]: </div>
                                <div class="mt-3 sm:pl-4">
                                    Select a visual option for the session
                                    <img src={step3} class="w-full" alt="">
                                    <div class="font-bold">Know more about the visual options:</div>
                                    <div class="ml-4">
                                        <div class="my-2">
                                            <button id="tree" class="text-[#bfedc1] border-2 py-2 px-6.5 cursor-pointer hover:bg-[#bfedc1] hover:text-black rounded">🌲 Tree</button>
                                            <Popover triggeredBy="#tree" class="w-full max-w-96 bg-black rounded ml-2">
                                                <div class="text-sm text-center font-bold text-[#CFF27E]">Tree</div>
                                                <img src={tree_png} class="w-full" alt="">
                                                <div class="text-sm">This visual option procedurally generates a random tree everytime you start a session.</div>
                                            </Popover>
                                        </div>
                                        <div class="my-3">
                                            <button id="flow" class="text-[#bfedc1] border-2 py-2 px-6.5 cursor-pointer hover:bg-[#bfedc1] hover:text-black rounded">🛶 Flow</button>
                                            <Popover triggeredBy="#flow" class="w-full max-w-96 bg-black rounded ml-2">
                                                <div class="text-sm text-center font-bold text-[#CFF27E]">Flow</div>
                                                <img src={flowgif} class="w-full" alt="">
                                                <div class="text-sm">This visual option has a guy who is rowing through the "Time River". </div>
                                            </Popover>
                                        </div>
                                        <div class="my-2">
                                            <button id="coffee" class="text-[#bfedc1] border-2 py-2 px-4 cursor-pointer hover:bg-[#bfedc1] hover:text-black rounded">☕ Coffee</button>
                                            <Popover triggeredBy="#coffee" class="w-full max-w-96 bg-black rounded ml-2">
                                                <div class="text-sm text-center font-bold text-[#CFF27E]">Coffee</div>
                                                <img src={coffee} class="w-full" alt="">
                                                <div class="text-sm">This visual option has a coffee mug that filles up over time. </div>
                                            </Popover>
                                        </div>
                                    </div>
                                </div>

                            </div>

                            <div class="mt-10">
                                <div class="font-bold text-[#bfedc1]">Step [4]:</div>
                                <div class="mt-3 sm:pl-4">
                                    Work! 
                                    <img src={flow} class="w-full" alt="">
                                    <div class="text-sm">Unfortunately notifications will appear only if you install the app.</div>
                                </div>

                            </div>
                        </div>
                    </div>
                </div>
                <section id="install-local" class="mt-24 mb-16 text-center flex justify-center">
                    <div class="max-w-lg">
                        <div class="mb-2  text-[#CFF27E]">Homeground</div>
                        <div class="text-3xl font-bold text-[#49beaa]">Install Pomossh Locally?</div>
                        <div class="mt-3">Install pomossh in your own device with a single bash script.</div>
                    </div>
                </section>

                <section id=":S2:" class="relative-z-5">
                    <div class="new-container z-10 ">
                        <div
                            class="border border-border-light bg-black py-8"
                        >
                            <div class="px-5 py-2">
                                To install pomossh locally run the following command.
                                <div class="my-6">
                                    <div class="mb-2 text-[#bfedc1] font-bold">Linux/MAC:</div>
                                    <div class="px-4 py-2 rounded bg-gray-800 text-sm">
                                        curl -sSL https://gist.githubusercontent.com/sairash/f07c0d194c755fdd6c4fe39d0010ec30/raw | bash
                                    </div>
                                </div>
        
                                <div class="mb-4">
                                    <div class=" text-[#bfedc1] font-bold">
                                        Windows:
                                    </div>
        
                                    <div class="mt-2 mb-5 px-4 py-2 rounded bg-gray-800 text-sm overflow-auto">
                                        curl -sSL https://gist.githubusercontent.com/sairash/d6ce0c6a627f932dd105f17209d1b0e2/raw/20c42bfbafb09bf495cda7a77fe33fcab0055e6a/install_pomo.ps1 | powershell -c -
                                    </div>
                                    or 
                                    <div class="mt-2">
                                        <div class=" text-[#bfedc1] font-bold">
                                            Install manually:
                                        </div>
            
                                        
                                        <div class="pl-4 mt-2">
                                            <div class="px-4 py-2 rounded bg-gray-800 text-sm">
                                                git clone https://github.com/sairash/pomossh
                                            </div>
                                            <div class="px-4 py-2 rounded bg-gray-800 text-sm mt-3">
                                               cd pomossh
                                            </div>
                                            <div class="px-4 py-2 rounded bg-gray-800 text-sm mt-3">
                                                go build
                                             </div>
                                        </div>
                                    </div>

                                    
                                    <div class="mt-8">
                                        and
                                        <div class=" text-[#bfedc1] font-bold mt-4">
                                            Run pomossh as client:
                                        </div>
            
                                        
                                        <div class="pl-4 mt-2">
                                            <div class="px-4 py-2 rounded bg-gray-800 text-sm">
                                                pomossh
                                            </div>
                                        </div>

                                        <div class=" text-[#bfedc1] font-bold mt-6">
                                            Run pomossh as server:
                                        </div>
            
                                        
                                        <div class="pl-4 mt-2">
                                            <div class="px-4 py-2 rounded bg-gray-800 text-sm">
                                                pomossh -ssh true
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                           
                        </div>
                    </div>
                     <div class="my-5 text-center">Made With ❤️ by <a href="https://sairashgautam.com.np" target="_blank" class="border-b-2 text-[#CFF27E]" rel="noopener noreferrer">Sairash</a>.</div>
                </section>
            </div>
        </section>
    </section>
</div>
