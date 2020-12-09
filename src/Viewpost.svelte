<script>
    import {onMount} from "svelte";

    let res = [];
    let title, body, count, thumbnail;
    let categorie = []
    let id = localStorage.getItem("id")
    fetch('https://api-m120.mailino.io/api/posts/' + id, {
        method: 'GET',
        headers: {
            'Content-Type': 'application/json',
            'Authorization': 'Bearer ' + localStorage.getItem('token')
        }

    }).then(result => {
        result.json().then(result => {
            title = result.title
            body = result.body
            thumbnail = result.thumbnail
            count = result.count
            categorie = result.categories
        })
    })
</script>
<main>
    <h1>{title}</h1>
    <p>Views: {count}</p>
    <p>categories:</p>
    {#each categorie as c,i}
    <p >{i+1}) {c.name}</p>
        {/each}
    <p id="body">{body}</p>
</main>
<style>
    h1, p{
        color:#ffffff;
    }
    #body{
        width: 50%;
        border-top: 1px solid #000000;
    }
</style>