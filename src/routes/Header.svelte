<script>
	import { page } from '$app/stores';
</script>

<header>
	<nav>
		<ul>
			<li aria-current={$page.url.pathname === '/' ? 'page' : undefined}>
				<a href="/">Home</a>
			</li>
			<li aria-current={$page.url.pathname === '/about' ? 'page' : undefined}>
				<a href="/about">About</a>
			</li>
			<li aria-current={$page.url.pathname.startsWith('/sverdle') ? 'page' : undefined}>
				<a href="/sverdle">Sverdle</a>
			</li>
		</ul>
	</nav>
</header>

<style>
	header {
		display: flex;
		justify-content: center;
		align-items: center;
		height: 3em;
		width: 100%;
		background: var(--background);
	}

	nav {
		display: flex;
		height: 100%;
		width: 100%;
		max-width: 600px;
	}

	ul {
		display: flex;
		height: 100%;
		width: 100%;
		list-style: none;
		margin: 0;
		padding: 0;
	}

	li {
		display: flex;
		height: 100%;
		width: 100%;
		position: relative;
	}

	li[aria-current='page'] a {
		color: var(--color-theme-1);
		z-index: 1;
	}

	li a::before {
		content: '';
		background-color: rgba(0, 0, 0, 0);
		inset: 0;
		position: absolute;
		z-index: -1;
		transition: background-color 0.25s ease-in-out;
	}

	li a::after {
		content: '';
		position: absolute;
		bottom: 0;
		left: 0;
		width: 100%;
		height: 0.2rem;
		background: rgba(0, 0, 0, 0);
		transition: background-color 0.25s ease-in-out;
	}

	li[aria-current='page'] a::before {
		content: '';
		background-color: rgba(0, 0, 0, 0.164);
		inset: 0;
		position: absolute;
		z-index: -1;
	}

	li[aria-current='page'] a::after {
		content: '';
		position: absolute;
		bottom: 0;
		left: 0;
		width: 100%;
		height: 0.2rem;
		background: var(--color-theme-1);
	}

	nav a {
		display: flex;
		justify-content: center;
		align-items: center;
		height: 100%;
		width: 100%;
		text-decoration: none;
		color: var(--color-text);
		transition: all 0.25s ease-in-out;
	}

	a:hover {
		color: var(--color-theme-1);
	}
</style>
