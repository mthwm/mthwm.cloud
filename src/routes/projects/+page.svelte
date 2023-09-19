<svelte:head>
	<title>Projects</title>
	<meta name="description" content="My projects" />
</svelte:head>

<div class="text-column">
    <h1>Projects</h1>

    <p>
        This page contains a list of my projects. I will add more projects as I make them.
    </p>

    <ul>
        <li>
            <a href="projects/shower">Shower</a>
        </li>
    </ul>
</div>

<style>
    ul {
        list-style: none;
        padding: 0;
    }

    li {
        margin-bottom: 0.5rem;
    }

    li a {
        text-decoration: none;
        color: var(--color-theme-1);
        position: relative;
        display: inline-block;
        width: 100%;
        height: 2rem;
        font-weight: bold;
        font-size: 1.2rem;
        line-height: 2rem;
        text-align: center;
        padding: 1rem 0;
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

    li a:hover::before {
        content: '';
        background-color: rgba(0, 0, 0, 0.164);
        inset: 0;
        position: absolute;
        z-index: -1;
    }

    li a:hover::after {
        content: '';
        position: absolute;
        bottom: 0;
        left: 0;
        width: 100%;
        height: 0.2rem;
        background: var(--color-theme-1);
    }

</style>
