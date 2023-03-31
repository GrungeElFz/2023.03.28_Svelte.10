<script>
	import { v4 as uuid } from 'uuid';
	import { getContext } from 'svelte';
	import formKey from './form-key';

	export let name;
	export let type = 'text';
	export let label = undefined;
	export let validate = undefined;

	const formStore = getContext(formKey);

	const id = uuid();
</script>

<div class="field">
	{#if label}
		<label for={id}>{label}</label>
	{/if}
	<input
		{id}
		{name}
		{type}
		placeholder={label}
		value={$formStore.values[name] || ''}
		on:input={(e) => {
			$formStore.values[name] = e.currentTarget.value;
		}}
	/>
</div>

<style>
	div.field {
		margin-bottom: 0.8rem;
	}
	label {
		display: block;
		font-size: 1rem;
		margin-bottom: 0.3rem;
	}
	input {
		height: 2rem;
		width: 20rem;
		max-width: 100%;
	}
</style>
