<script>
	import Invoice from '../components/Invoice.svelte';
	import Data from '../components/Data.svelte';

	import { setContext } from 'svelte';

	let data = {
		invoiceNumber: '001',
		logo_url: 'https://cdn.pixabay.com/photo/2014/02/27/16/10/flowers-276014_1280.jpg',
		invoiceType: 'Invoice',
		issueDate: '06/6/2021',
		dueDate: '10/6/2021',
		senderDetails: {
			name: 'Nagendra Allam',
			address1: ' 1234 Main Street,',
			address2: 'Suite 1234,',
			city: 'Anytown',
			state: 'ST',
			zip: '12345',
			email: 'nagendraallam@icloud.com'
		},
		recipientDetails: {
			name: 'James Bond',
			address: ' 1234 Main Street,',
			address2: ' Suite 1234, ',
			city: 'Anytown',
			state: 'ST',
			zip: '12345',
			email: ' james@bond.com'
		},
		item: [
			{
				name: 'Rifle - [u24394] Sniper - [u24394] 9mm',
				description: ' 9mm Sniper Rifle - [u24394]',
				quantity: 1,
				price: 568.99
			}
		],
		total: 568.99,
		notes: ''
	};

	setContext('data', data);
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<button
		class="border-2 pl-4 pr-4 p-2 border-red-600 m-3 fixed top-2 right-2"
		on:click={() => {
			var printContents = document.getElementById('invoice').innerHTML;
			var originalContents = document.body.innerHTML;

			// OPEN NEW tab with print contents and print it
			var printWindow = window.open('', '', 'height=400,width=800');
			printWindow.document.write(
				'<html><head><title>Print it!</title><link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">'
			);
			printWindow.document.write('</head><body >');
			printWindow.document.write(printContents);
			printWindow.document.write('</body></html>');
			printWindow.document.close();
			printWindow.print();
		}}>Print Invoice</button
	>
	<Data />
	<Invoice />
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}

	h1 {
		width: 100%;
	}

	.welcome {
		display: block;
		position: relative;
		width: 100%;
		height: 0;
		padding: 0 0 calc(100% * 495 / 2048) 0;
	}

	.welcome img {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		display: block;
	}
</style>
