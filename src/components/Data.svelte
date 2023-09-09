<script>
	import { getContext, setContext } from 'svelte';

	let data = getContext('data');

	function updateData(key, value) {
		let spilitKey = key.split('.');
		if (spilitKey.length > 1) {
			data[spilitKey[0]][spilitKey[1]] = value;
		} else {
			data[key] = value;
		}

		console.log(data);

		setContext('data', data);
	}
</script>

<div class="bg-slate-500 w-[30vw] mr-2 fixed top-0 left-0 h-[100vh]">
	<h1>Details</h1>
	<div class="flex flex-col">
		<label for="name">Name</label>
		<input
			type="text"
			name="name"
			id="name"
			value={data.senderDetails.name}
			on:change={(e) => updateData('senderDetails.name', e.target.value)}
		/>
	</div>
	<div class="flex flex-col">
		<label for="address1">Address 1</label>
		<input
			type="text"
			name="address1"
			id="address1"
			value={data.senderDetails.address1}
			on:change={(e) => updateData('address1', e.target.value)}
		/>
	</div>
</div>
