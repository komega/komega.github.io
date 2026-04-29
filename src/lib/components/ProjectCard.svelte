<script lang="ts">
	let {
		name,
		downloads,
		tech,
		link
	} = $props<{
		name: string;
		downloads: string;
		tech: string;
		link: string;
	}>();
</script>

<a
	href={link}
	target="_blank"
	rel="noopener noreferrer"
	class="block border border-gray-200 dark:border-gray-700 rounded-lg p-6 hover:shadow-lg bg-white dark:bg-gray-800/40 hover:bg-gray-50 dark:hover:bg-gray-800"
>
	<h3 class="text-xl font-bold text-gray-900 dark:text-gray-100 mb-2">{name}</h3>
	<p class="text-gray-600 dark:text-gray-400 mb-4 flex items-center gap-2">
		<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4"></path></svg>
		{downloads}
	</p>
	<span class="inline-block bg-gray-100 dark:bg-gray-700 text-gray-800 dark:text-gray-200 text-sm px-3 py-1 rounded-full font-medium">
		{tech}
	</span>
</a>
