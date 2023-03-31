<script>
	import { setContext, createEventDispatcher } from 'svelte';
	import { writable } from 'svelte/store';
	import formKey from './form-key';

	export let initialValues = {};

	const dispatch = createEventDispatcher();
	const form = writable({ values: initialValues, errors: {} });

	setContext(formKey, form);
</script>

<form
	on:submit|preventDefault={() => {
		dispatch('submit', $form.values);
	}}
>
	<slot />
</form>
