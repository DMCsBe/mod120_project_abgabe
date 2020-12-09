<script>
    let res = [];
    let title,active, categorie, body, count, thumbnail;
    let id = localStorage.getItem("id")
    "https://api-m120.mailino.io/api/categories"
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
        })
    })
    fetch('https://api-m120.mailino.io/api/categories', {
        method: 'GET',
        headers: {
            'Content-Type': 'application/json',
            'Authorization': 'Bearer ' + localStorage.getItem('token')
        }

    }).then(result => {
        result.json().then(result => {
            res = result
            console.log(result)
        })
    })
    function update(){
        active = active === "true";
        fetch('https://api-m120.mailino.io/api/posts/' + id, {
            method: 'PUT',
            headers: {
                'Content-Type': 'application/json',
                'Authorization': 'Bearer ' + localStorage.getItem('token')
            },
            body: JSON.stringify({
                title: title,
                body: body,
                thumbnail: "",
                categorie: [categorie],
                active: active
            })

        }).then(result => {
            result.json().then(result => {
            })
        })
    }
    $: console.log(categorie)
</script>
<main>
    <p>This Post has {count} Views</p>
    <form>
        <div class="center">
            <label for="input1">title</label>
            <input autocomplete="off" type="text" id="input1" bind:value={title}>
            <label for="input2">body</label>
            <textarea id="input2" style="resize: none;" bind:value={body}></textarea>
            <label class="categorie" for="categorie">Choose Categorie</label>
            <select class="categorie" bind:value={categorie} name="categorie" id="categorie">
                {#each res as r, i}
                <option>{r.name}</option>
                    {/each}
            </select>
            <label id="active1" for="active">Active</label><br>
            <select bind:value={active} name="active" id="active">
                <option value="true">Yes</option>
                <option value="false">No</option>
            </select>
        </div>
        <div>
            <button on:click={update} type="button">Change</button>
        </div>
    </form>
</main>
<style>
    label{
        color: #ffffff;
    }
    div{
        text-align: center;
    }
    .center{
        margin-top: 50px;
    }
    textarea{
        width: 70%;
        height: 400px;
    }
    #input1{
        width: 70%;
    }
    p{
        color: #ffffff;
    }
    .categorie{
        margin-left: -150px;
    }
    #active{
        margin-right: -150px;
        margin-top: -100px;
    }
    #active1{
        margin-right: -150px;
        margin-top: -58px;
    }
    button{
        margin-top: 30px;
        margin-left: 30px;
    }
</style>