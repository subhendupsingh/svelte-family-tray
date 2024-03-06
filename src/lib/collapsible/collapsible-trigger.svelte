<script lang='ts'>
	import anime from "animejs";
    export let destructive = false;
</script>

<button on:click class="tray-button {destructive ? "text-red-500 !bg-red-100" : ""}">
    <slot></slot>
</button>

<style lang="postcss">
    .tray-button {
        @apply w-full bg-gray-100 py-3 px-4 rounded-xl text-sm font-semibold flex gap-2.5 items-center;
    }

    .icon {
        @apply h-4 w-4 stroke-[4] text-gray-400 group-hover:text-gray-600;
    }
</style>