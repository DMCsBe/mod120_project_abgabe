<script>
    import { fade } from 'svelte/transition';
    let active_true = [];
    fetch('https://api-m120.mailino.io/api/posts?active=true', {
        method: 'GET',
        headers:{
            'Content-Type': 'application/json',
            'Authorization': 'Bearer ' + localStorage.getItem('token')
        }

    }).then(result => {
        result.json().then(result => {
            active_true = result
        })
    })
</script>
<main>
    <h1>All Posts</h1>
    <table style="width:95%">
        <tr id="table" transition:fade>
            <th>Title</th>
            <th>active</th>
            <th></th>
        </tr>
        {#each active_true as r, i}
            <tr class="table_row" transition:fade>
                <td>{r.title}</td>
                <td>true</td>
                <td>View</td>
            </tr>
        {/each}
    </table>
</main>
<style>
    h1{
        color: #ffffff;
        text-align: center;
    }
    td, th{
        text-align: center;
        color: #ffffff;
    }
    #table{
        background-color: #333;
    }
    .table_row{
        background-color: #999999;
    }
</style>