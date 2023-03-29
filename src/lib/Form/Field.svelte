<script>
	import { v4 as uuid } from 'uuid';

	export let name;
	export let type = 'text';
	export let label = undefined;
	export let validate = undefined;

	const id = uuid();
</script>

<div>
	{#if label}
		<label for={id}>{label}</label>
	{/if}
	<input {id} {name} {type} placeholder={label} />
</div>
