<script>
	import { getContext } from 'svelte';

	let store = getContext('data');

	let data = $store;

	store.subscribe((d) => {
		data = d;
	});

	function updateVals(key, value) {
		let splitKey = key.split('.');

		if (splitKey[0] === 'item') {
			store.update((d) => {
				let updatedArray = [...d.item];
				updatedArray[splitKey[1]] = { ...updatedArray[splitKey[1]], [splitKey[2]]: value };

				if (d !== undefined) {
					return {
						...d,
						item: updatedArray
					};
				}
			});

			return;
		}

		if (splitKey.length > 1) {
			store.update((d) => {
				if (d !== undefined)
					return { ...d, [splitKey[0]]: { ...d[splitKey[0]], [splitKey[1]]: value } };
			});
		} else
			store.update((d) => {
				if (d !== undefined) return { ...d, [key]: value };
			});
	}
</script>

<div
	class="bg-slate-800 w-[25vw] mr-2 fixed top-0 left-0 h-[100vh] overflow-y-auto overflow-x-hidden pl-4"
>
	<h1 class="text-xl text-white mt-10 underline">Edit Details</h1>
	<h3 class="text-xl w-full text-white mt-2 underline">Invoice Details</h3>
	<div class="flex flex-col">
		{#each Object.entries(data) as [key, value]}
			{#if typeof value !== 'object' && value !== 'array'}
				<label class="text-white w-full" for="invoiceName">{key}</label>
				<input
					type="text"
					name="invoiceName"
					class="w-[20vw] h-8 border-2 border-slate-500 rounded-md"
					id="invoiceName"
					{value}
					on:change={(e) => updateVals(`${key}`, e.target.value)}
				/>
			{/if}
		{/each}
	</div>

	<h3 class="text-xl w-full text-white underline mt-4">Sender Details</h3>
	<div class="flex flex-col">
		{#each Object.entries(data.senderDetails) as [key, value]}
			<label class="text-white w-full" for="senderName">{key}</label>
			<input
				type="text"
				name="senderName"
				id="senderName"
				class="w-[20vw] h-8 border-2 border-slate-500 rounded-md"
				{value}
				on:change={(e) => updateVals(`senderDetails.${key}`, e.target.value)}
			/>
		{/each}
	</div>
	<h3 class="text-xl w-full text-white underline mt-4">Receiver Details</h3>
	<div class="flex flex-col">
		{#each Object.entries(data.recipientDetails) as [key, value]}
			<label class="text-white w-full" for="receiverName">{key}</label>
			<input
				type="text"
				name="receiverName"
				id="receiverName"
				class="w-[20vw] h-8 border-2 border-slate-500 rounded-md"
				{value}
				on:change={(e) => updateVals(`recipentDetails.${key}`, e.target.value)}
			/>
		{/each}
	</div>
	<h3 class="text-xl w-full text-white underline mt-4">Item Details</h3>
	<div class="flex flex-col">
		{#each data.item as item, i}
			<div class="flex flex-col">
				{#each Object.entries(item) as [key, value]}
					<label class="text-white w-full" for="itemName">{key}</label>
					<input
						type="text"
						name="itemName"
						class="w-[20vw] h-8 border-2 border-slate-500 rounded-md"
						id="itemName"
						{value}
						on:change={(e) => updateVals(`item.${i}.${key}`, e.target.value)}
					/>
				{/each}
			</div>
		{/each}
	</div>
</div>
