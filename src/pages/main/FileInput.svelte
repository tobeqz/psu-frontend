<script lang="ts">
    export let file_contents: string = "";

    let filename = "Select File"

    async function newFile(e) {
        console.log('Updating')
        const file = e.target.files.item(0) as File

        filename = file.name

        if (filename.length > 15) {
            filename = filename.substring(0, 15) + '...'
        }
        file_contents = await file.text()
    }
</script>

<style>
    input {
        width: .1px;
        height: .1px;
        opacity: 0;
        position: absolute;
    }

    div.container {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
        width: 250px;
    }

    div.file-input > .actual-button {
        width: 100px;
        height: 30px;
        padding: 7px 20px;
        background-color: #098352;
        border-radius: 20px;
        font-size: .7rem;
        font-weight: bold;
        color: white;
        cursor: pointer;
        transition: .2s;
        text-overflow: ellipsis;
    }

    div.file-input > .actual-button:hover {
        box-shadow: 1px 10px 19px -14px rgba(255,255,255,0.75);
        -webkit-box-shadow: 1px 10px 19px -14px rgba(255,255,255,0.75);
        -moz-box-shadow: 1px 10px 19px -14px rgba(255,255,255,0.75);
    }
</style>

<div class="container">
    <p>File</p>
    <div class="file-input">
        <input id="file" type="file" on:change={newFile}>
        <label for="file" class="actual-button">{filename}</label>
    </div>
</div>