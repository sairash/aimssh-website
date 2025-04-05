<script lang="ts">
	import "../app.css";
	import logo from "$lib/assets/logo.png";
	import logoText from "$lib/assets/logo-text.png";

	let { children } = $props();
	let title = "<POMO SSH>";
</script>

<div class="flex justify-center font-mono">
	<div class="w-full max-w-5xl ">
		<div
			class="sticky top-0 z-header z-40 flex min-h-header-height items-center border-b border-border-light border-gray-600 bg-[#000000b3] backdrop-blur-[8px]"
		>
			<div class="new-container w-full">
				<div class="px-3 md:px-4 py-2 flex justify-between">
					<div class="flex gap-2">
						<img src={logo} class="h-16" alt="Logo" />
						<div class="mt-1 text-[#49beaa]">
							<img src={logoText} alt="Pomo SSH" class="h-9 -ml-1">
							<div class="text-sm">Applications in Terminal</div>
						</div>
					</div>
					<div class="mt-4">
						<a
							href="https://github.com/sairash/pomossh"
							class="py-1 px-3 font-semibold text-sm bg-white text-black rounded flex gap-1"
							target="_blank"
							>
							<span class="mt-0.5">Github</span> 
							<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-4">
								<path stroke-linecap="round" stroke-linejoin="round" d="M13.5 6H5.25A2.25 2.25 0 0 0 3 8.25v10.5A2.25 2.25 0 0 0 5.25 21h10.5A2.25 2.25 0 0 0 18 18.75V10.5m-10.5 6L21 3m0 0h-5.25M21 3v5.25" />
							  </svg>
							  
							</a
						>
					</div>
				</div>
			</div>
		</div>
		<div class="">
			{@render children()}
		</div>
	</div>
</div>
