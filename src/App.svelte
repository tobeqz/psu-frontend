<script>
    import { Router, Route } from "svelte-routing";

    import MainPage from "./pages/main/Index.svelte"
    import Login from "./pages/login/Index.svelte"
</script>

<Router>
    <Route path="" component={Login} />
    <Route path="obfuscate" component={MainPage} />
    <Route path="login" component={Login} />
</Router>