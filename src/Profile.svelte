<script>
    function delete_user() {
        fetch('https://api-m120.mailino.io/api/users/self', {
            method: 'GET',
            headers: {
                'Content-Type': 'application/json',
                'Authorization': 'Bearer ' + localStorage.getItem('token')
            }

        }).then(result => {
            result.json().then(result => {
                localStorage.setItem("uuid", result.uuid)
            })
        })
        fetch('https://api-m120.mailino.io/api/users/' + localStorage.getItem("uuid"), {
            method: 'DELETE',
            headers: {
                'Content-Type': 'application/json',
                'Authorization': 'Bearer ' + localStorage.getItem('token')
            }

        }).then(result => {
            result.json().then(result => {
                if(!result.message){
                    localStorage.setItem("uuid", "")
                    localStorage.setItem("login", "false")
                    localStorage.setItem("doing", "")
                    localStorage.setItem("url", "/")
                    localStorage.setItem("password", "")
                    localStorage.setItem("email", "")
                    location.reload()
                }
            })
        }).catch(err =>{
            console.log(err)
        })
    }
</script>
<main>
    <div>
        <button on:click={delete_user}>DELETE PROFIL</button>
    </div>
</main>
<style>
    button{
        background-color: red;
}
    div{
        text-align: center;
    }
</style>