<svelte:head>
    <title>Shower ~ mthwm</title>
    <meta name="description" content="Shower is a web app that allows you to create and share presentations." />
</svelte:head>

<script>
    let text = 'loading...';
    fetchAndUpdateTheText();

    function fetchAndUpdateTheText() {
        fetch('http://mthwm.cloud:3000/api/db/lastShower')
                    .then(res => res.json())
                    .then(data => {
                        const now = Math.floor(Date.now() / 1000);
                        const secondsSinceLastShower = now - data;
                        const days = Math.floor(secondsSinceLastShower / 86400);
                        const hours = Math.floor((secondsSinceLastShower % 86400) / 3600);
                        const minutes = Math.floor(((secondsSinceLastShower % 86400) % 3600) / 60);
                        const seconds = Math.floor(((secondsSinceLastShower % 86400) % 3600) % 60);

                        text = `${days} days, ${hours} hours, ${minutes} minutes, ${seconds} seconds`;
                    });
    }

    setInterval(() => {
        fetchAndUpdateTheText();
    }, 1000)
</script>

<div class="text-column">
    <h1>Shower</h1>

    <p>
        Project shower is a simple counter that counts the days since I last took a shower.  
    </p>

    <p>
        It uses a redis database to store the timestamp of the last shower.
        It also uses a simple API to retrieve the data from the redis database and allows me to reset it.
    </p>

    <div class="counter">{text}</div>
</div>

<style>
    .counter {
        font-size: 2rem;
        font-weight: bold;
        margin-top: 1rem;
        position: relative;
        display: inline-block;
        width: 100%;
        height: 4rem;
        line-height: 4rem;
        text-align: center;
        padding: 1rem 0;
        margin-top: 2rem;
    }
</style>