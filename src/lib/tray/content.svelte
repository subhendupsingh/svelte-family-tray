<script lang='ts'>
    import * as Collapsible from "$lib/collapsible";
	import anime from "animejs";
	import { ShieldCheck, Table } from "lucide-svelte";

    const revealCollapsedContent = (e: Event) => {
        const target = e.target as HTMLElement;
        const colapsedContent = target.nextElementSibling;
        colapsedContent?.classList.remove("hidden");
        anime({
            targets: colapsedContent,
            duration: 500,
            maxHeight: [0,100,300,600,900],
            easing: 'linear',
            begin: () => {
                toggleTrayButtons("hide");
            }
        }).play();
    }

    const collapseContent = (e: Event) => {
        const target = e.target as HTMLElement;
        const parentNode = target.closest("#collapsible-content") as HTMLElement;
        
        let tl = anime.timeline({
            easing: 'linear',
            duration: 200
        });

        tl.add({
            targets: parentNode,
            maxHeight: [100,75,50,0],
            complete: () => {
                toggleTrayButtons("show");
            }
        });

        tl.play();
    }

    const toggleTrayButtons = (state: "hide"|"show") => {
        const buttons = document.getElementsByClassName("tray-button");
        for (let index = 0; index < buttons.length; index++) {
            const button = buttons[index] as HTMLElement;
            button.style.display = state == "hide" ? "none" : "flex";
        }
    }
</script>

<div id="buttons" class="mt-4 flex flex-col gap-3">
    <Collapsible.Root>
        <Collapsible.Trigger on:click={(e)=>revealCollapsedContent(e)}>
            <ShieldCheck class="h-5 w-5 stroke-[2] text-gray-400 group-hover:text-gray-600" />
            View Private Key
        </Collapsible.Trigger>
        <Collapsible.Content>
            <h1 class="text-xl font-semibold mb-2">Private Key</h1>
            <p class="border-b border-[#F5F4F5] pb-4 font-medium leading-6 text-[#989998]">
                Your Private Key is the key used to back up your wallet. Keep it secret and secure at all times. Don't share it with anyone.
            </p>

            <ul class="mb-8 mt-4 space-y-3"><li class="flex items-center gap-2 text-sm font-medium text-[#989998]"><svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="h-[22px] w-[22px]"><path stroke-linecap="round" stroke-linejoin="round" d="M9 12.75L11.25 15 15 9.75m-3-7.036A11.959 11.959 0 013.598 6 11.99 11.99 0 003 9.749c0 5.592 3.824 10.29 9 11.623 5.176-1.332 9-6.03 9-11.622 0-1.31-.21-2.571-.598-3.751h-.152c-3.196 0-6.1-1.248-8.25-3.285z"></path></svg>Keep your Secret Phrase safe</li><li class="flex items-center gap-2 text-sm font-medium text-[#989998]"><svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="h-[22px] w-[22px]"><path stroke-linecap="round" stroke-linejoin="round" d="M2.25 8.25h19.5M2.25 9h19.5m-16.5 5.25h6m-6 2.25h3m-3.75 3h15a2.25 2.25 0 002.25-2.25V6.75A2.25 2.25 0 0019.5 4.5h-15a2.25 2.25 0 00-2.25 2.25v10.5A2.25 2.25 0 004.5 19.5z"></path></svg>Don't share it with anyone else</li><li class="flex items-center gap-2 text-sm font-medium text-[#989998]"><svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="h-[22px] w-[22px]"><path stroke-linecap="round" stroke-linejoin="round" d="M18.364 18.364A9 9 0 005.636 5.636m12.728 12.728A9 9 0 015.636 5.636m12.728 12.728L5.636 5.636"></path></svg>If you lose it, we can't recover it</li></ul>
            <div class="flex gap-4">
                <button on:click={(e)=>collapseContent(e)} class="h-10 grow rounded-full  bg-[#F0F1F4] font-semibold text-black transition-transform focus:scale-90 focus-visible:shadow-focus-ring-button active:scale-90">Cancel</button>
                <button on:click={(e)=>collapseContent(e)} class="flex h-10 grow  items-center justify-center gap-2 rounded-full bg-[#00B2FF] font-semibold text-white transition-transform focus:scale-90 focus-visible:shadow-focus-ring-button active:scale-90"><svg width="20px" height="20px" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M7 3H5C3.89543 3 3 3.89543 3 5V7" stroke="#fff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"></path><path d="M17 3H19C20.1046 3 21 3.89543 21 5V7" stroke="#fff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"></path><path d="M16 8L16 10" stroke="#fff" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"></path><path d="M8 8L8 10" stroke="#fff" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"></path><path d="M9 16C9 16 10 17 12 17C14 17 15 16 15 16" stroke="#fff" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"></path><path d="M12 8L12 13L11 13" stroke="#fff" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"></path><path d="M7 21H5C3.89543 21 3 20.1046 3 19V17" stroke="#fff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"></path><path d="M17 21H19C20.1046 21 21 20.1046 21 19V17" stroke="#fff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"></path></svg>Reveal</button>
            </div>
        </Collapsible.Content>
    </Collapsible.Root>
    
    <Collapsible.Root>
        <Collapsible.Trigger on:click={(e)=>revealCollapsedContent(e)}>
            <Table class="h-5 w-5 stroke-[2] text-gray-400 group-hover:text-gray-600" />
            View Recovery Phase
        </Collapsible.Trigger>
        <Collapsible.Content>
            <h1 class="text-xl font-semibold mb-2">Private Key</h1>
            <p class="border-b border-[#F5F4F5] pb-4 font-medium leading-6 text-[#989998]">
                Your Private Key is the key used to back up your wallet. Keep it secret and secure at all times. Don't share it with anyone.
            </p>

            <ul class="mb-8 mt-4 space-y-3"><li class="flex items-center gap-2 text-sm font-medium text-[#989998]"><svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="h-[22px] w-[22px]"><path stroke-linecap="round" stroke-linejoin="round" d="M9 12.75L11.25 15 15 9.75m-3-7.036A11.959 11.959 0 013.598 6 11.99 11.99 0 003 9.749c0 5.592 3.824 10.29 9 11.623 5.176-1.332 9-6.03 9-11.622 0-1.31-.21-2.571-.598-3.751h-.152c-3.196 0-6.1-1.248-8.25-3.285z"></path></svg>Keep your Secret Phrase safe</li><li class="flex items-center gap-2 text-sm font-medium text-[#989998]"><svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="h-[22px] w-[22px]"><path stroke-linecap="round" stroke-linejoin="round" d="M2.25 8.25h19.5M2.25 9h19.5m-16.5 5.25h6m-6 2.25h3m-3.75 3h15a2.25 2.25 0 002.25-2.25V6.75A2.25 2.25 0 0019.5 4.5h-15a2.25 2.25 0 00-2.25 2.25v10.5A2.25 2.25 0 004.5 19.5z"></path></svg>Don't share it with anyone else</li><li class="flex items-center gap-2 text-sm font-medium text-[#989998]"><svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="h-[22px] w-[22px]"><path stroke-linecap="round" stroke-linejoin="round" d="M18.364 18.364A9 9 0 005.636 5.636m12.728 12.728A9 9 0 015.636 5.636m12.728 12.728L5.636 5.636"></path></svg>If you lose it, we can't recover it</li></ul>
            <div class="flex gap-4">
                <button on:click={(e)=>collapseContent(e)} class="h-10 grow rounded-full  bg-[#F0F1F4] font-semibold text-black transition-transform focus:scale-90 focus-visible:shadow-focus-ring-button active:scale-90">Cancel</button>
                <button on:click={(e)=>collapseContent(e)} class="flex h-10 grow  items-center justify-center gap-2 rounded-full bg-[#00B2FF] font-semibold text-white transition-transform focus:scale-90 focus-visible:shadow-focus-ring-button active:scale-90"><svg width="20px" height="20px" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M7 3H5C3.89543 3 3 3.89543 3 5V7" stroke="#fff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"></path><path d="M17 3H19C20.1046 3 21 3.89543 21 5V7" stroke="#fff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"></path><path d="M16 8L16 10" stroke="#fff" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"></path><path d="M8 8L8 10" stroke="#fff" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"></path><path d="M9 16C9 16 10 17 12 17C14 17 15 16 15 16" stroke="#fff" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"></path><path d="M12 8L12 13L11 13" stroke="#fff" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"></path><path d="M7 21H5C3.89543 21 3 20.1046 3 19V17" stroke="#fff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"></path><path d="M17 21H19C20.1046 21 21 20.1046 21 19V17" stroke="#fff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"></path></svg>Reveal</button>
            </div>
        </Collapsible.Content>
    </Collapsible.Root>

    <Collapsible.Root>
        <Collapsible.Trigger on:click={(e)=>revealCollapsedContent(e)} destructive={true}>
            <Table class="h-5 w-5 stroke-[2]  group-hover:text-gray-600" />
            Remove Wallet
        </Collapsible.Trigger>
        <Collapsible.Content>
            <h1 class="text-xl font-semibold mb-2">Private Key</h1>
            <p class="border-b border-[#F5F4F5] pb-4 font-medium leading-6 text-[#989998]">
                Your Private Key is the key used to back up your wallet. Keep it secret and secure at all times. Don't share it with anyone.
            </p>

            <ul class="mb-8 mt-4 space-y-3"><li class="flex items-center gap-2 text-sm font-medium text-[#989998]"><svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="h-[22px] w-[22px]"><path stroke-linecap="round" stroke-linejoin="round" d="M9 12.75L11.25 15 15 9.75m-3-7.036A11.959 11.959 0 013.598 6 11.99 11.99 0 003 9.749c0 5.592 3.824 10.29 9 11.623 5.176-1.332 9-6.03 9-11.622 0-1.31-.21-2.571-.598-3.751h-.152c-3.196 0-6.1-1.248-8.25-3.285z"></path></svg>Keep your Secret Phrase safe</li><li class="flex items-center gap-2 text-sm font-medium text-[#989998]"><svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="h-[22px] w-[22px]"><path stroke-linecap="round" stroke-linejoin="round" d="M2.25 8.25h19.5M2.25 9h19.5m-16.5 5.25h6m-6 2.25h3m-3.75 3h15a2.25 2.25 0 002.25-2.25V6.75A2.25 2.25 0 0019.5 4.5h-15a2.25 2.25 0 00-2.25 2.25v10.5A2.25 2.25 0 004.5 19.5z"></path></svg>Don't share it with anyone else</li><li class="flex items-center gap-2 text-sm font-medium text-[#989998]"><svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="h-[22px] w-[22px]"><path stroke-linecap="round" stroke-linejoin="round" d="M18.364 18.364A9 9 0 005.636 5.636m12.728 12.728A9 9 0 015.636 5.636m12.728 12.728L5.636 5.636"></path></svg>If you lose it, we can't recover it</li></ul>
            <div class="flex gap-4">
                <button on:click={(e)=>collapseContent(e)} class="h-10 grow rounded-full  bg-[#F0F1F4] font-semibold text-black transition-transform focus:scale-90 focus-visible:shadow-focus-ring-button active:scale-90">Cancel</button>
                <button on:click={(e)=>collapseContent(e)} class="flex h-10 grow  items-center justify-center gap-2 rounded-full bg-[#00B2FF] font-semibold text-white transition-transform focus:scale-90 focus-visible:shadow-focus-ring-button active:scale-90"><svg width="20px" height="20px" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M7 3H5C3.89543 3 3 3.89543 3 5V7" stroke="#fff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"></path><path d="M17 3H19C20.1046 3 21 3.89543 21 5V7" stroke="#fff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"></path><path d="M16 8L16 10" stroke="#fff" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"></path><path d="M8 8L8 10" stroke="#fff" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"></path><path d="M9 16C9 16 10 17 12 17C14 17 15 16 15 16" stroke="#fff" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"></path><path d="M12 8L12 13L11 13" stroke="#fff" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"></path><path d="M7 21H5C3.89543 21 3 20.1046 3 19V17" stroke="#fff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"></path><path d="M17 21H19C20.1046 21 21 20.1046 21 19V17" stroke="#fff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"></path></svg>Reveal</button>
            </div>
        </Collapsible.Content>
    </Collapsible.Root>
</div>