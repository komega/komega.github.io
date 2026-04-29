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
	class="block border border-gray-200 rounded-lg p-6 hover:shadow-lg transition-shadow duration-300 bg-white"
>
	<h3 class="text-xl font-bold text-gray-900 mb-2">{name}</h3>
	<p class="text-gray-600 mb-4 flex items-center gap-2">
		<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4"></path></svg>
		{downloads}
	</p>
	<span class="inline-block bg-gray-100 text-gray-800 text-sm px-3 py-1 rounded-full font-medium">
		{tech}
	</span>
</a>
