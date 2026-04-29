<script lang="ts">
	import { onMount } from 'svelte';

	let {
		name,
		score
	} = $props<{
		name: string;
		score: number;
	}>();

	let width = $state(0);

	onMount(() => {
		const timer = setTimeout(() => {
			width = score * 10;
		}, 100);
		return () => clearTimeout(timer);
	});
</script>

<div class="mb-4 group">
	<div class="flex justify-between mb-1">
		<span class="text-gray-700 dark:text-gray-300 font-medium">{name}</span>
		<span class="text-gray-500 dark:text-gray-500 text-sm">{score}/10</span>
	</div>
	<div class="w-full bg-gray-200 dark:bg-gray-700 rounded-full h-2.5 overflow-hidden">
		<div
			class="bg-blue-600 dark:bg-blue-500 h-2.5 rounded-full duration-500"
			style="width: {width}%"
		></div>
	</div>
</div>
