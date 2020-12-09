<script>
    export let active_true = [];
    import { fade } from 'svelte/transition';
    localStorage.setItem("doing", "edit")
    localStorage.setItem("url", "home")
    fetch('https://api-m120.mailino.io/api/users/self', {
        method: 'GET',
        headers:{
            'Content-Type': 'application/json',
            'Authorization': 'Bearer ' + localStorage.getItem('token')
        }

    }).then(result => {
        result.json().then(result => {
            localStorage.setItem("uuid", result.uuid)
        })
        fetch('https://api-m120.mailino.io/api/users/' + localStorage.getItem("uuid") +'/posts', {
            method: 'GET',
            headers: {
                'Content-Type': 'application/json',
                'Authorization': 'Bearer ' + localStorage.getItem('token')
            }

        }).then(result => {
            result.json().then(result => {
                active_true = result
            })
        }).catch(err => {
            console.log(err)
        })
    })
    function seturl(id){
        localStorage.setItem("url","edit/" + id)
        localStorage.setItem("id", id)
        location.reload()
    }
    function delete_post(id){
        fetch('https://api-m120.mailino.io/api/posts/' + id, {
            method: 'DELETE',
            headers: {
                'Content-Type': 'application/json',
                'Authorization': 'Bearer ' + localStorage.getItem('token')
            },
            body:{
                'id': id
            }

        })
    }
</script>
<main>
<h1>Your Posts</h1>
    <table style="width:95%">
        <tr id="table" transition:fade>
            <th>Title</th>
            <th>Views</th>
            <th></th>
            <th></th>
        </tr>
        {#each active_true as r, i}
        <tr class="table_row" transition:fade>
            <td>{r.title}</td>
            <td>{r.count}</td>
            <td><button on:click={() =>seturl(r.id)}>EDIT</button></td>
            <td><button id="delete" on:click={() =>delete_post(r.id)}>DELETE</button></td>
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
    #delete{
        background-color: red;
    }
</style>