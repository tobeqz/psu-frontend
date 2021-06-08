<script lang="ts">
	import Toggle from "./Toggle.svelte"
	import BytecodeSelect from "./BytecodeSelect.svelte"
	import FileInput from "./FileInput.svelte"
	import SubmitButton from "./SubmitButton.svelte"
	import Download from './DownloadButton.svelte'

	// Option variables
	let encrypt_all_strings = false
	let enhanced_output = false
	let maximum_security = false
	let no_super_operators = false
	let disable_macros = false
	let compressed_output = false
	let premium_format = false
	let control_flow = true // enabled by default in psu lol so yes better leave it on like this and its secure
	let const_encryption = false
	let enchanced_const_encrypt = false
	let fake_constants = "2000"
	let antiEQ_hooking = false
	let randomize_opcode = true // by default it should be enabled as control flow obfuscation

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
				EnhancedConstantEncryption: enchanced_const_encrypt,
				MaximumSecurityEnabled: maximum_security,
				ControlFlowObfuscation: control_flow,
				ConstantEncryption: const_encryption,
				DisableSuperOperators: no_super_operators,
				DisableAllMacros: disable_macros,
				CompressedOutput: compressed_output,
				PremiumFormat: premium_format,
				FakeConstants: fake_constants,
				AntiEQHook: antiEQ_hooking,
				OpcodeRandomization: randomize_opcode,
				ByteCodeMode: bytecode,
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
		<Toggle name="Enhanced Constant Encryption" bind:value={enchanced_const_encrypt} />
		<Toggle name="Maximum Security" bind:value={maximum_security} />
		<Toggle name="Control flow Obfuscation" bind:value={control_flow} />
		<Toggle name="Constant Encryption" bind:value={const_encryption} />
		<Toggle name="Disable Super Operators" bind:value={no_super_operators} />
		<Toggle name="Disable All Macros" bind:value={disable_macros} />
		<Toggle name="Compressed Output" bind:value={compressed_output} />
		<Toggle name="Premium Output" bind:value={premium_format} />
		<Toggle name="Anti EQ Hooking" bind:value={antiEQ_hooking} />
		<Toggle name="OPcode randomization" bind:value={randomize_opcode} />
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
