<script>
	import { setContext, createEventDispatcher } from 'svelte';
	import { writable } from 'svelte/store';
	import formKey from './form-key';

	export let initialValues = {};

	const dispatch = createEventDispatcher();
	const formStore = writable({ values: initialValues, errors: {} });

	setContext(formKey, formStore);
</script>

<form
	on:submit|preventDefault={() => {
		if (Object.keys($formStore.errors).length === 0) {
			dispatch('submit', $formStore.values);
		}
	}}
>
	<slot />
</form>
