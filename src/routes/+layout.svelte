<script lang="ts">
	let { children } = $props();
</script>

<nav>
	<ul>
		<li><a href="/">九九乘法表</a></li>
		<li><a href="/clock">時鐘</a></li>
	</ul>
</nav>

{@render children()}

<style lang="scss">
	nav {
		background-color: #2eb738;
		color: #fff;

		ul {
			margin: 0 auto;
			max-width: 1280px;
			display: flex;
			flex-direction: row;

			li {
				padding: 12px 0;
				padding-right: 24px;
			}
		}
	}
</style>
