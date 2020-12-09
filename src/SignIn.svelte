<script>
    let  subscription, subscribe, firstname, lastname, street, streetnr, plz, city, country = ""
    let email = localStorage.getItem("email")
    let password = localStorage.getItem("password")
    let error = localStorage.getItem("error")
    localStorage.setItem("error", "")
    function signup(){
        if (subscribe === "1"){
            subscription = 1
        }else if(subscribe === "2"){
            subscription = 2
        }else{
            subscription = 3
        }
        fetch('https://api-m120.mailino.io/api/users', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({
                email: email,
                subscription: subscription,
                firstName: firstname,
                lastName: lastname,
                password: password,
                street: street,
                streetNr: streetnr,
                zip: plz,
                city: city,
                country: country,
                role: "user"
            })

        }).then(result => {
            result.json().then(result => {
                console.log(result)
                if (!result.message){
                    localStorage.setItem("url","/")
                    localStorage.setItem("doing","edit")
                    alert("Account created, you can now Log In")
                }else{
                    localStorage.setItem("error", result.message)
                    localStorage.setItem("url", "sign_in")
                    location.reload()
                }
            })
        })
    }
    let width;
    $:{
        localStorage.setItem("password", password)
        localStorage.setItem("email", email)
    }
</script>
<svelte:window bind:innerWidth={width}/>
<main>

    <form>

        <div class="center">

            <label class="middle" for="input1">firstname</label>
            <input autocomplete="off" class="middle" type="text" id="input1" bind:value={firstname}>
            <label class="middle" for="input2">lastname</label>
            <input autocomplete="off" class="middle" type="text" id="input2" bind:value={lastname}><br>
            <label class="middle" for="input3">email</label>
            <input autocomplete="off" class="middle" type="text" id="input3" bind:value={email}>
            <label class="middle" for="input4">password</label>
            <input autocomplete="off" class="middle" type="password" id="input4" bind:value={password}><br>
            <label class="middle" for="input5">street</label>
            <input autocomplete="off" class="middle" type="text" id="input5" bind:value={street}>
            <label class="middle" for="input6">streetnr</label>
            <input autocomplete="off" class="middle" type="number" id="input6" bind:value={streetnr}><br>
            <label class="middle" for="input7">plz</label>
            <input autocomplete="off" class="middle" type="number" id="input7" bind:value={plz}>
            <label class="middle" for="input8">city</label>
            <input autocomplete="off" class="middle" type="text" id="input8" bind:value={city}><br>
            <label class="middle" for="input9">country</label>
            <input autocomplete="off" class="middle" type="text" id="input9" bind:value={country}>
            <label class="middle" for="dropdown1">subscription</label>
            <select bind:value={subscribe} name="active" id="dropdown1">
                <option value="1">Standart</option>
                <option value="2">Premium</option>
                <option value="3">None</option>
            </select>
            <br>
            <p id="error">{error}</p>
            <button on:click={signup} type="button">Sign Up</button>
        </div>
        <br>
    </form>

</main>
<style>
    .center{
        text-align:center
    }
    label{
        color: #ffffff;
    }
    #error{
        color: red;
    }
</style>