<script>
	import { setContext } from 'svelte';
	import { writable } from 'svelte/store';
	import formKey from './form-key';

	export let initialValues = {};
	const form = writable({ values: initialValues, errors: {} })

	setContext(formKey, form);
</script>

<form>
	<slot />
</form>
