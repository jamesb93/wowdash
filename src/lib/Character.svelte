<script>
    import { onMount } from 'svelte';
    import { seasonTable, classColours } from '$lib/data.js';
    import { msConvert } from '$lib/time.js';
    export let name;
    export let realm;

    const url = `https://raider.io/api/v1/characters/profile?region=us&realm=${realm}&name=${name}&fields=mythic_plus_ranks%2Cmythic_plus_recent_runs%2Cmythic_plus_scores_by_season%3Acurrent`
    let data;
    let classColour ;
    let classColourStyle;
    let containerBackground;

    onMount(async() => {
        const response = await fetch(url);
        data = await response.json();
        classColour = classColours[data.class];
        classColourStyle = `color: rgba(${classColour.r * 0.5}, ${classColour.g * 0.5}, ${classColour.b * 0.5}, 1.0)`
        containerBackground = `background-color: rgba(${classColour.r}, ${classColour.g}, ${classColour.b}, 0.3)`
        console.log(data)
    })

</script>

<div class='container' style={containerBackground}>
    {#if data}
        <div>
            <p id='name'>{data.name}</p>
            <img id="profile" src={data.thumbnail_url} alt="profile pic">
            <p style={classColourStyle}>{data.active_spec_name} {data.class} </p>      
            <a href={data.profile_url}>Raider IO</a>
        </div>
    
        {#each data.mythic_plus_scores_by_season as d}
            <span class='emph'>{seasonTable[d.season]}:</span> {d.scores.all}
        {/each}

        <p class='emph'>Recent Runs:</p>
        <ul id="runs">
            {#each data.mythic_plus_recent_runs as run}
                <li><a target='_blank' href={run.url}>{run.short_name} - {run.mythic_level}</a></li>
            {/each}
        </ul>

        
    {:else}
        loading...
    {/if}
</div>


<style lang="scss">

    .emph {
        font-weight:bold;
    }

    #name {
        font-weight: bold;
        font-style: italic;
    }
    
    .container {
        border: 1px solid grey;
        border-radius: 15px;
        min-width: 10%;
        max-width: 25%;
        justify-content: center;
        align-content: center;
        align-items: center;
        margin: 10px;
        padding: 10px;
    }

    #profile {
        width: 50%;
        margin: auto;
        display: block;
    }

    ul {
        display: block;
        list-style-type: none;
        margin: 0;
        padding: 0;
    }
</style>