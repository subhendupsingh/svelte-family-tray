<script lang='ts'>
	import anime from "animejs";
	import { X } from "lucide-svelte";

    const closeTray = () => {
        const tray = document.getElementById("tray");

         anime({
            targets: "#tray-container",
            translateY: [0, 300],
            duration: 300,
            easing: 'easeInOutExpo',
            complete: function(anim) {
                tray?.classList.add("hidden");
            }
        }).play();
    }
</script>

<div id="header" class="py-2 flex justify-between items-center">
    <h1 class="font-semibold text-base text-gray-800">Options</h1>
    <button on:click={()=>closeTray()} class="bg-gray-50 rounded-full p-1.5 group">
        <X class="h-4 w-4 stroke-[4] text-gray-400 group-hover:text-gray-600" />
    </button>
</div>