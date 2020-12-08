<script>
    let active_true = []
    let title, body,count, thumbnail;
    let id = localStorage.getItem("id")
    fetch('https://api-m120.mailino.io/api/posts/' + id, {
        method: 'GET',
        headers: {
            'Content-Type': 'application/json',
            'Authorization': 'Bearer ' + localStorage.getItem('token')
        }

    }).then(result => {
        result.json().then(result => {
            active_true = result
            title = result.title
            body = result.body
            thumbnail = result.thumbnail
            count = result.count
        })
    })
</script>
<main>
    <p>This Post has {count} Views</p>
    <form>
        <div class="center">
            <label for="input1">title</label>
            <input autocomplete="off" type="text" id="input1" bind:value={title}>
        </div>
    </form>
</main>
<style>
    label{
        color: #ffffff;
    }
    .center{
        text-align: center;
    }
</style>