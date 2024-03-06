<script lang='ts'>
    import anime from 'animejs';
    import * as Tray from "$lib/tray";
	import { ExternalLink, Twitter, TwitterIcon } from 'lucide-svelte';

    const openTray = () => {
        const tray = document.getElementById("tray");
        tray?.classList.remove("hidden");
        tray?.classList.add("flex");

        let tl = anime.timeline({
            easing: 'easeOutExpo',
            duration: 750
        });

        tl.add({
            targets: "#backdrop",
            opacity: [0,1],
            duration: 30,
            easing: "linear"
        }).add({
            targets: "#tray-container",
            translateY: [0],
            duration: 300,
            easing: 'cubicBezier(.5, .05, .1, .3)',
        });

        tl.play();
    }
</script>

<div class="bg-slate-50 h-screen w-screen flex flex-col justify-center items-center gap-4">
    <div class="flex flex-col gap-4 justify-between items-center">
        <h1 class="text-left text-lg text-gray-600 font-semibold">Family's tray system</h1>
        <a href="https://twitter.com/subhendupsingh" class="text-sm text-blue-500 bg-blue-100 px-4 py-2 rounded-lg flex items-center gap-2">
            <TwitterIcon class="h-4 w-4" />
            <span>subhendupsingh</span>
            <ExternalLink class="h-4 w-4" />
        </a>
    </div>

    <div class="bg-white shadow-sm border-[1px] border-gray-200 rounded-lg flex justify-center items-center m-6 max-w-[692px] h-96 w-[90%] lg:w-1/2 lg:m-0">
        <button on:click={()=> openTray()} class="shadow-sm border-[1px] border-gray-200 rounded-md pointer-events-auto px-4 py-2 text-sm font-semibold hover:bg-gray-50 transition-colors duration-300">Open</button>
    </div>

    <div class="absolute h-full w-full flex justify-center" id="tray">
        <div class=" bg-black/30 h-full w-full z-10" id="backdrop"></div>
        <div class="bg-white bottom-3 p-6 absolute z-20 rounded-[2rem] w-96 max-w-sm" id="tray-container">
            <!-- Header -->
            <Tray.Header />

            <!-- Divider -->
            <Tray.Divider />
            
            <!-- Content -->
            <Tray.Content />
        </div>
    </div>
</div>