<script lang="ts">
	let {
		time,
		title,
		subtitle,
		tasks = []
	} = $props<{
		time: string;
		title: string;
		subtitle: string;
		tasks?: string[];
	}>();
</script>

<div class="flex flex-col md:flex-row gap-4 md:gap-8 lg:gap-12 group">
	<div class="md:w-1/4 flex-shrink-0">
		<span class="inline-block bg-blue-100 dark:bg-blue-900/30 text-blue-800 dark:text-blue-300 px-3 py-1 rounded-full text-sm font-semibold whitespace-nowrap">
			{time}
		</span>
	</div>
	<div class="md:w-3/4">
		<h3 class="text-xl font-bold text-gray-900 dark:text-gray-100">{title}</h3>
		<p class="text-blue-600 dark:text-blue-400 font-medium mb-2">{subtitle}</p>
		{#if tasks && tasks.length > 0}
			<ul class="list-disc list-inside text-gray-600 dark:text-gray-400 space-y-1">
				{#each tasks as task}
					<li>{task}</li>
				{/each}
			</ul>
		{/if}
	</div>
</div>
