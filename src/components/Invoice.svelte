<script>
	import { getContext } from 'svelte';

	let d = getContext('data');
	let data = $d;
	let total = 0;
	d.subscribe((d) => {
		data = d;
		// count all the items and calculate the total
		if (d !== undefined) {
			let count = 0;
			d.item.forEach((item) => {
				count += parseFloat(item.price) * parseFloat(item.quantity);
			});
			total = count;
		}
	});

	// function to format a number to currency and add decimal places
	function formatNumber(num) {
		return num.toFixed(2).replace(/\d(?=(\d{3})+\.)/g, '$&,');
	}
	let email = 'nagendraallam.com';
</script>

<div id="invoice" class="bg-white ml-[30vw] w-[60vw] p-4 rounded-sm flex flex-col mt-28 mb-28">
	<section id="company-info" class="flex flex-col w-full">
		<div id="invoice-header" class="flex flex-row w-full justify-between">
			<div id="company-row-details" class="flex flex-row">
				<div class="">
					<img alt="logo" src={data.logo_url} class="w-16 h-16" />
				</div>
				<div id="company-details" class="flex flex-col ml-4 z-10 text-md">
					<h2 class="text-xl">
						<b>
							{data.senderDetails?.name}
						</b>
					</h2>
					<h2>{data.senderDetails?.address1}</h2>
					<h2>{data.senderDetails?.address2}</h2>
					<h2>
						{data.senderDetails?.city}, {data.senderDetails?.state}-
						{data.senderDetails?.zip}
					</h2>
					<h2>{data.senderDetails?.email}</h2>
				</div>
			</div>
			<div class="flex flex-row">
				<h2>
					<b>
						{data.invoiceType} &nbsp;
					</b>
				</h2>
				<h2>
					<b>
						#{data.invoiceNumber}
					</b>
				</h2>
			</div>
		</div>
		<div class="flex flex-col items-end w-full">
			<div id="invoice-issue-date" class="w-fit flex flex-row">
				<h2><b>Date :&nbsp; </b></h2>
				<h2>
					{data.issueDate}
				</h2>
			</div>
			<div id="invoice-due-date" class="w-fit flex flex-row">
				<h2><b> Due Date :&nbsp; </b></h2>
				<h2>
					{data.dueDate}
				</h2>
			</div>
		</div>
	</section>
	<section class="w-full flex flex-row justify-between text-lg mb-2 mt-4">
		<div id="sender-details" class="w-[50%]">
			<h2 class="text-xl underline"><b>From</b></h2>
			<h2>{data.senderDetails?.name}</h2>
			<h2>
				{data.senderDetails?.city}, {data.senderDetails?.state}
				{data.senderDetails?.zip}
			</h2>
			<h2>{data.senderDetails?.email}</h2>
		</div>
		<div id="recipient-details" class="w-[50%]">
			<h2 class="text-xl underline"><b>To</b></h2>
			<h2>{data.recipientDetails?.name}</h2>
			<h2>
				{data.recipientDetails?.city}, {data.recipientDetails?.state}
				{data.recipientDetails?.zip}
			</h2>
			<h2>{data.recipientDetails?.email}</h2>
		</div>
	</section>
	<section>
		<div id="invoice-items">
			<h2
				class="text-center border-t-2 border-l-2 border-r-2 border-slate-900"
				style={'background-color: rgb(148 163 184);'}
			>
				<b> Invoice Items </b>
			</h2>
			<div class="flex flex-row justify-between" style="background-color: #97a3b6;">
				<h2 class="w-[25%] border-l-2 border-b-2 border-t-2 text-center border-slate-900">
					<b> Item </b>
				</h2>
				<h2 class="w-[25%] border-l-2 border-b-2 border-t-2 text-center border-slate-900">
					<b> Quantity </b>
				</h2>
				<h2 class="w-[25%] border-l-2 border-b-2 border-t-2 text-center border-slate-900">
					<b> Price </b>
				</h2>
				<h2
					class="w-[25%] border-l-2 border-b-2 border-t-2 border-r-2 text-center border-slate-900"
				>
					<b> Total </b>
				</h2>
			</div>
			{#if data.item !== undefined}
				{#each data.item as item}
					<div class="w-full flex flex-row justify-between">
						<h2 class="w-[25%] border-l-2 border-b-2 text-center border-slate-900">
							{item.name}
						</h2>
						<h2 class="w-[25%] border-l-2 border-b-2 text-center bg-slate-200 border-slate-900">
							{item.quantity}
						</h2>
						<h2 class="w-[25%] border-l-2 border-b-2 text-center border-slate-900">
							{item.price}
						</h2>
						<h2
							class="w-[25%] border-l-2 border-b-2 border-r-2 text-center bg-slate-200 border-slate-900"
						>
							${formatNumber(parseFloat(item.price) * parseFloat(item.quantity))}
						</h2>
					</div>
				{/each}
			{/if}
		</div>
	</section>
	<section id="invoice-total" class="flex justify-end mt-10">
		<div id="invoice-total-main-div" class="mr-6">
			<h2 class="bg-slate-400 border-slate-900 border-t-2 border-l-2 border-r-2 p-2 text-center">
				<b> Total </b>
			</h2>
			<h2 class="border-2 border-slate-800 p-2 text-center">${formatNumber(total)}</h2>
		</div>
	</section>
	<section id="invoice-footer" class="absolute bottom-0">
		<div id="invoice-notes" class="flex flex-col">
			<h2>Notes</h2>
			<h2>{data.notes}</h2>
			<h5>
				Please make sure to pay the invoice before the due date. If you have any questions, please
				contact us at
				<a
					href="mailto:
                {email}
                ">{email}</a
				>
			</h5>
		</div>
	</section>
</div>
