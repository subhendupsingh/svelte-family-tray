<script lang='ts'>
    import anime from 'animejs';
    import * as Tray from "$lib/tray";

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

<div class="bg-slate-50 h-screen w-screen flex justify-center items-center">
    <div class="bg-white shadow-sm border-[1px] border-gray-200 rounded-lg flex justify-center items-center mx-auto my-12 max-w-[692px] h-96 w-full lg:w-1/2 m-6 lg:m-0">
        <button on:click={()=> openTray()} class="shadow-sm border-[1px] border-gray-200 rounded-md pointer-events-auto px-4 py-2 text-sm font-semibold hover:bg-gray-50 transition-colors duration-300">Open</button>
    </div>

    <div class="absolute h-full w-full flex" id="tray">
        <div class=" bg-black/30 h-full w-full z-10" id="backdrop"></div>
        <div class="bg-white bottom-3 left-[40%] p-6 absolute z-20 rounded-[2rem] w-96 max-w-sm" id="tray-container">
            <!-- Header -->
            <Tray.Header />

            <!-- Divider -->
            <Tray.Divider />
            
            <!-- Content -->
            <Tray.Content />
        </div>
    </div>
</div>