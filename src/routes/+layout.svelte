<script>
	import './styles.css';
</script>

<div class="app">
	<main>
		<slot />
	</main>

	<footer>
		<p>
			visit <a href="https://nagendraallam.com">nagendraallam.com</a> to find more amazing tools.
		</p>
	</footer>
</div>

<style>
	.app {
		display: flex;
		flex-direction: column;
		min-height: 100vh;
	}

	footer {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: 12px;
	}

	footer a {
		font-weight: bold;
	}

	@media (min-width: 480px) {
		footer {
			padding: 12px 0;
		}
	}
</style>
