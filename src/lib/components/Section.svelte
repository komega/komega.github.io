<script lang="ts">
	import type { Snippet } from 'svelte';

	let { title, children } = $props<{
		title: string;
		children: Snippet;
	}>();
</script>

<section class="mb-10">
	<h2 class="text-2xl font-bold text-gray-800 border-b-2 border-blue-600 pb-2 mb-6 uppercase tracking-wider">
		{title}
	</h2>
	<div class="text-gray-700 leading-relaxed space-y-4">
		{@render children()}
	</div>
</section>
