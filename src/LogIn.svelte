<script>
    let error = localStorage.getItem("error")
    localStorage.setItem("error", "")
    let email = localStorage.getItem("email")
    let password = localStorage.getItem("password")
    localStorage.setItem("doing", "login")
    function seturl() {
            fetch('https://api-m120.mailino.io/api/auth/login', {
                method: 'POST',
                headers:{'Content-Type': 'application/json'},
                body: JSON.stringify({
                    email: email,
                    password: password
                })
            }).then(result => {
                result.json().then(result =>{
                    if(result.token){
                        localStorage.setItem('token', result.token);
                        localStorage.setItem('login', "true");
                        console.log("ok")
                        location.reload()
                    }else {
                        localStorage.setItem("login", "now")
                        localStorage.setItem("error", "e-mail or passoword wrong")
                        localStorage.setItem("password", "")
                        localStorage.setItem("email", "")
                        location.reload()
                    }
                })
            }).catch(err => {
                console.log(err);
            })

    }
    $:{
        localStorage.setItem("email", email)
        localStorage.setItem("password", password)
    }
</script>
<main>
    <form>
        <div class="center">
            <label class="middle" for="input1">e-mail</label>
            <input autocomplete="off" class="middle" type="text" id="input1" bind:value={email}>
            <label class="middle" for="input2">Password</label>
            <input autocomplete="off" class="middle" type="password" id="input2" bind:value={password}>
            <br>
            <p id="error_show">{error}</p>
            <button on:click={seturl} type="button">Log In</button>
        </div>
    </form>
</main>
<style>
.center{
    text-align:center
}
label{
    color: #ffffff;
}
#error_show{
    color: red;
}
</style>