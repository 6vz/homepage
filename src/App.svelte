<script lang="ts">
    import { fade } from 'svelte/transition';

    import { fade } from 'svelte/transition';

    let loaded = false;
    setTimeout(() => {
        loaded = true;
    }, 500);

    let date = new Date();
    let hour = date.getHours();

    let greeting = 'Good morning';
    if (hour > 12) {
        greeting = 'Good afternoon';
    }
    if (hour > 18) {
        greeting = 'Good evening';
    }
    if (hour > 22) {
        greeting = 'Good night';
    }
    // get name of day of the week, us locale
    let day = date.toLocaleDateString('en-US', { weekday: 'long' });
    let welcome = [
        "How's your [] going?",
        "Today it's a beautiful []",
        '[] - great day for surfing the web',
        "How's your [] treating you?",
        "Today it's a beautiful [] afternoon.",
        '[] - great day for catching up on work emails.',
        "How's your [] going so far?",
        "Today it's a beautiful [] morning.",
        '[] - great day for lazy Netflix binging.',
        "How's your [] shaping up?",
        "Today it's a beautiful [] evening.",
        '[] - great day for running errands.',
        "How's your [] looking?",
        "Today it's a beautiful [] sunset.",
        '[] - great day for starting fresh.',
    ];
    let random = Math.floor(Math.random() * welcome.length);
    let welcomeMessage = welcome[random].replace('[]', day);

    let placeholder_poss = [
        'Facebook',
        'YouTube',
        'Google',
        'Gmail',
        'Amazon',
        'Weather',
        'Netflix',
        'Translate',
        'WhatsApp',
        'Instagram',
        'Yahoo',
        'Twitter',
        'eBay',
        'Maps',
        'Wikipedia',
        'LinkedIn',
        'Hotmail',
        'Pinterest',
        'PayPal',
        'Outlook',
        'News',
        'Bank of America',
        'CNN',
        'Apple',
        'Instagram login',
        'Craigslist',
        'Target',
        'ESPN',
        'WalMart',
        'CNN news',
        'Delta',
        'Home Depot',
        'Best Buy',
        'Google Maps',
        'Netflix login',
        'Gmail login',
        'Lowes',
        'MSN',
    ];
    let random_poss = placeholder_poss[Math.floor(Math.random() * placeholder_poss.length)];
    random_poss = '🔍 ' + random_poss;

    function handleSearch(searchEngine: string) {
        let search = (document.getElementById('search-bar') as HTMLInputElement).value;
        let baseUrl = '';
        if (searchEngine === 'google') {
            baseUrl = 'https://www.google.com/search?q=';
        } else if (searchEngine === 'duckduckgo') {
            baseUrl = 'https://duckduckgo.com/?q=';
        } else if (searchEngine === 'perplexity') {
            baseUrl = 'https://perplexity.ai/search?q=';
        }
        window.location.href = baseUrl + search;
    }
</script>

<div id="content">
    <div class="position-absolute top-50 start-50 translate-middle" id="box" transition:fade>
        <h1 class="title">{greeting}</h1>
        <p class="subtitle">{welcomeMessage}</p>
        <br />
        <input class="input" id="search-bar" type="text" placeholder={random_poss} />
        <br /><br /><br />
        <div class="container whatsize text-center">
            <div class="row">
                <div class="col">
                    <img src="https://i.imgur.com/DUCTmkN.png" on:click={() => handleSearch('google')} class="icon" alt="" />
                </div>
                <div class="col">
                    <img src="https://i.imgur.com/z0GJTor.png" on:click={() => handleSearch('duckduckgo')} class="icon" alt="" />
                </div>
                <div class="col">
                    <img src="https://i.imgur.com/ib02W6Q.png" on:click={() => handleSearch('perplexity')} class="icon" alt="" />
                </div>
            </div>
        </div>
    </div>
</div>
