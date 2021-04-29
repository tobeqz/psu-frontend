<script lang="ts">
	import Toggle from "./Toggle.svelte"
	import BytecodeSelect from "./BytecodeSelect.svelte"
	import FileInput from "./FileInput.svelte"
	import SubmitButton from "./SubmitButton.svelte"
	import Download from './DownloadButton.svelte'

	let encrypt_all_strings = false
	let enhanced_output = false
	let maximum_security = false
	let no_super_operators = false
	let disable_macros = false
	let compress_output = false
	let premium_format = false

	let bytecode = "Default"
	let file_content = ""

	let download_link = "#"

	async function submit() {
		const params = {
			script: file_content,
			key: localStorage.getItem("key"),
			options: {
				EncryptAllStrings: encrypt_all_strings,
				EnhancedOutput: enhanced_output,
				MaximumSecurity: maximum_security,
				NoSuperOperators: no_super_operators,
				DisableMacros: disable_macros,
				CompressOutput: compress_output,
				PremiumFormat: premium_format,
				ByteCodeMode: bytecode
			}
		}

		const response = await fetch("https://api.psu.dev/obfuscate", {
			method: "POST",
			headers: {
				"Content-Type": "application/json"
			},
			body: JSON.stringify(params)
		})	

		if (response.status == 200) {
			const obfuscated_file = JSON.parse(await response.text()).data
			const blob = new Blob([obfuscated_file], {type: "text/plain"})

			download_link = window.URL.createObjectURL(blob)
		}
	}
</script>

<main>
	<h1>PSU Obfuscate</h1>
	<div>
		<Toggle name="Encrypt All Strings" bind:value={encrypt_all_strings} />
		<Toggle name="Enhanced Output" bind:value={enhanced_output} />
		<Toggle name="Maximum Security" bind:value={maximum_security} />
		<Toggle name="No Super Operators" bind:value={no_super_operators} />
		<Toggle name="Disable Macros" bind:value={disable_macros}  />
		<Toggle name="Compress Output" bind:value={compress_output} />
		<Toggle name="Premium Format" bind:value={premium_format} />
		<BytecodeSelect bind:selected={bytecode} />
		<FileInput bind:file_contents={file_content} />
	</div>

	<SubmitButton on:click={submit} />
	<br/>
	<Download link={download_link} />
</main>

<style>
	main {
		text-align: center;
		width: 70vw;
		margin: 0 auto;
	}

	div {
		display: flex;
		flex-direction: column;
		width: 200px;
		padding: 20px;
		align-items: center;
		justify-self: space-between; 
		margin: 0 auto;
	}
</style>