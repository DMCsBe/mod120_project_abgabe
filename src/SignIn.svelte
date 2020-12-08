<script>
    let error, firstname, lastname, email, password, street, streetnr, plz, city, country = ""
    function signup(){

    }
    let width;
</script>
<svelte:window bind:innerWidth={width}/>
<main>

    <form>

        <div class="center">

            <label class="middle" for="input1">firstname</label>
            <input autocomplete="off" class="middle" type="text" id="input1" bind:value={firstname}>
            <label class="middle" for="input2">lastname</label>
            <input autocomplete="off" class="middle" type="password" id="input2" bind:value={lastname}><br>
            <label class="middle" for="input3">email</label>
            <input autocomplete="off" class="middle" type="password" id="input3" bind:value={email}>
            <label class="middle" for="input4">password</label>
            <input autocomplete="off" class="middle" type="password" id="input4" bind:value={password}><br>
            <label class="middle" for="input5">street</label>
            <input autocomplete="off" class="middle" type="password" id="input5" bind:value={street}>
            <label class="middle" for="input6">streetnr</label>
            <input autocomplete="off" class="middle" type="password" id="input6" bind:value={streetnr}><br>
            <label class="middle" for="input7">plz</label>
            <input autocomplete="off" class="middle" type="password" id="input7" bind:value={plz}>
            <label class="middle" for="input8">city</label>
            <input autocomplete="off" class="middle" type="password" id="input8" bind:value={city}><br>
            <label class="middle" for="input9">country</label>
            <input autocomplete="off" class="middle" type="password" id="input9" bind:value={country}>
            <label class="middle" for="dropdown1">subscription</label>
            <input autocomplete="off" class="middle" type="password" id="dropdown1">
            <br>
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
</style>
{#if width>700}
    <style>
        label{
            display: inline;
        }
    </style>
{/if}