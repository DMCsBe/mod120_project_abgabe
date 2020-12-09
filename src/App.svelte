<script>
    import Home from "./Home.svelte"
    import LogIn from "./LogIn.svelte"
    import Viewpost from "./Viewpost.svelte"
    import Editpost from "./Editpost.svelte"
    import SignIn from "./SignIn.svelte"
    import Overview from "./Overview.svelte"
    import Welcome from "./Welcome.svelte"
    import Profile from "./Profile.svelte"
    import {Router, Link, Route} from "svelte-routing";
    let login_now =localStorage.getItem("login")
    let doing = localStorage.getItem("doing")
    let width;
    let url = localStorage.getItem("url")
    if (login_now === "now" && doing === "login") {
        url = "login"
    }else if (login_now === "true" && doing === "login"){
        url = "home"
    }
    function logout(){
        localStorage.setItem("login", "false")
        localStorage.setItem("token", "")
        localStorage.setItem("doing", "login")
        localStorage.setItem("url", "/")
        location.reload()
    }

</script>
<svelte:window bind:innerWidth={width}/>
<main>
    <header>
        <nav>
            <Router url="{url}">
            <ul id="navlist">

                {#if localStorage.getItem("login") !== "true"}

                    <li id="navli3"><Link to="login"><p class="navli">Login</p></Link></li>
                    <li id="navli6"><Link to="sign_in"><p class="navli">Sign Up</p></Link></li>


                    {:else}

                    <li id="navli1"><Link to="home"><p class="navli">Home</p></Link></li>
                    <li id="navli2"><Link to="blogoverview"><p class="navli">Blog Overview</p></Link></li>
                    <li on:click={logout} id="navli5"><Link to="/"><p class="navli">Logout</p></Link></li>
                    <li id="navli4"><Link to="profile"><p class="navli">Profile</p></Link></li>

                {/if}
            </ul>
            <div>
                <Route path="/"><Welcome /></Route>
                <Route path="login" component="{LogIn}" />
                <Route path="sign_in" component="{SignIn}" />
                <Route path="home" component="{Home}" />
                <Route path="blogoverview" component="{Overview}" />
                <Route path="profile" component="{Profile}" />
                <Route path="edit/:id" component="{Editpost}"/>
                <Route path="view/:id" component="{Viewpost}"/>
            </div>
                </Router>
        </nav>
    </header>
</main>

<style>

    :root{
        background-color: #666666;
    }
    #navlist {
        list-style-type: none;
        margin: 0;
        padding: 0;
        overflow: hidden;
        background-color: #333;
    }

    li {
        float: left;
    }
    #navli4, #navli5{
        float: right;
    }

    .navli {
        display: block;

        color: white;
        text-align: center;
        margin-bottom: -10px;
        margin-top: -10px;
        padding: 30px 15px 30px 15px;
        text-decoration: none;
    }


    .navli:hover {
        background-color: #111;
    }
</style>