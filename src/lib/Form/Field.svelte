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
			const value = e.currentTarget.value;
			if (validate && validate(value)) {
				$formStore.errors[name] = validate(value, label);
			} else {
				delete $formStore.errors[name];
			}
			$formStore.values[name] = value;
		}}
	/>
	{#if $formStore.errors[name]}
		<p class="error">{$formStore.errors[name]}</p>
	{/if}
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
