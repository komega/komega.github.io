<script lang="ts">
	let {
		name,
		score
	} = $props<{
		name: string;
		score: number;
	}>();
</script>

<div class="mb-4">
	<div class="flex justify-between mb-1">
		<span class="text-gray-700 font-medium">{name}</span>
		<span class="text-gray-500 text-sm">{score}/10</span>
	</div>
	<div class="w-full bg-gray-200 rounded-full h-2.5">
		<div
			class="bg-blue-600 h-2.5 rounded-full"
			style="width: {score * 10}%"
		></div>
	</div>
</div>
