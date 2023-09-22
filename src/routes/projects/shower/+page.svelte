<svelte:head>
    <title>mthwm ~ shower</title>
    <meta name="description" content="Shower is a web app that allows you to create and share presentations." />
</svelte:head>

<script>
    import IoMdRefresh from 'svelte-icons/io/IoMdRefresh.svelte';
    import IoIosArrowRoundBack from 'svelte-icons/io/IoIosArrowRoundBack.svelte'
    import { onMount } from "svelte";

    $: text = 'loading...';
    let lastShower = 0;
    let counter = 0;
    
    onMount(async () => {
        await fetch('http://mthwm.cloud:3000/api/db/lastShower')
        .then(res => res.json())
        .then(data => {
            lastShower = data;
        });
    });

    async function fetchAndUpdateTheText() {
        
        if (counter >= 60) {
            counter = 0;
            await fetch('http://mthwm.cloud:3000/api/db/lastShower')
                .then(res => res.json())
                .then(data => {
                    lastShower = data;          
                });
        }
        

        const now = Math.floor(Date.now() / 1000);
        const secondsSinceLastShower = now - lastShower;
        const days = Math.floor(secondsSinceLastShower / 86400);
        const hours = Math.floor((secondsSinceLastShower % 86400) / 3600);
        const minutes = Math.floor(((secondsSinceLastShower % 86400) % 3600) / 60);
        const seconds = Math.floor(((secondsSinceLastShower % 86400) % 3600) % 60);

        text = `${days} days, ${hours} hours, ${minutes} minutes, ${seconds} seconds`;
        counter++;
    }

    setInterval(() => {
        fetchAndUpdateTheText();
    }, 1000)
</script>

<div class="text-column">
    <div>
        <a href="/projects" class="back"><IoIosArrowRoundBack /></a>
    </div>
    <h1>Shower</h1>

    <p>
        Project shower is a simple counter that counts the days since I last took a shower.  
    </p>

    <p>
        It uses a redis database to store the timestamp of the last shower.
        It also uses a simple API to retrieve the data from the redis database and allows me to reset it.
    </p>

    <div class="counter">{text}</div>

    <button class='icon' title="Refresh" on:click={async () => {
        await fetch('http://mthwm.cloud:3000/api/db/lastShower')
        .then(res => res.json())
        .then(data => {
            lastShower = data;
        });
    }}><IoMdRefresh /></button>
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

    .back {
        position: fixed;
        top: 0;
        left: 0;
        margin-top: 0.5rem;
        margin-left: 1rem;
        width: 32px;
        height: 32px;
        color: white;
        cursor: pointer;
        transition: all 0.3s ease-in-out; 
    }

    .back:hover {
        color: var(--color-theme-1);
        width: 48px;
        height: 48px;
    }
    
    .icon {
    color: white;
    background: none;
    border: none;
    width: 64px;
    height: 64px;
    margin: 0 auto;
    cursor: pointer;
    transition: all 0.3s ease-in-out;
    transform: rotate(0deg);
    
  }

    .icon:hover {
        color: var(--color-theme-1);
        transform: rotate(360deg);
    }
</style>