<script lang="ts">
import { onMount } from "svelte";


    let key = "";

    function checkEnter(key) {
        if (key.key == "Enter") {
            submit()
        }
    }

    function submit() {
        localStorage.setItem("key", key)

        window.location.pathname += "/obfuscate"
    }

    onMount(() => {
        if (localStorage.getItem("key") && window.location.pathname != "/login" && window.location.pathname != "/psu-frontend/login") {
            window.location.pathname = '/obfuscate'
        }
    })
</script>

<style>
    .container {
        text-align: center;
    }

    input[type="password"] {
        text-align: center;
        padding: 5px;
        width: 300px;
        border-radius: 5px;
        border: solid 2px #d1d1d1;
        outline: none;
        background-color: rgba(0, 0, 0, 0);
        color: #d1d1d1;
    }

    input[type="submit"] {
        padding: 5px;
        width: 150px;
        height: 30px;
        background-color: #098352;
        border-radius: 15px;
        border: none;
        outline: none;
        color: #d1d1d1;
        font-weight: bold;
        cursor: pointer;
        transition: transform .2s;
    }

    input[type="submit"]:hover {
        transform: scale(1.1, 1.1);
    }
</style>

<div class="container">
    <h1>Please enter your API key:</h1>
    <input type="password" on:keydown={checkEnter} bind:value={key}>
    <br/><br/>
    <input type="submit" value="Submit" on:click={submit}>
</div>