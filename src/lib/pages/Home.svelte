<script>
	import Button from '../Button.svelte';

	let values = {
		username: '',
		email: '',
		password: ''
	};
	let errors = {};
	let isSubmitting = false;

	function validate() {
		const errors = {};

		if (!values.username) {
			errors.username = 'The Username is required.';
		}
		if (!values.email) {
			errors.email = 'The Email is required.';
		}
		if (values.email && !/^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(values.email)) {
			errors.email = 'The Email is invalid.';
		}
		if (!values.password) {
			errors.password = 'The Password is required.';
		}

		return errors;
	}
</script>

<form
	on:submit|preventDefault={() => {
		errors = validate();
		if (Object.keys(errors).length === 0) {
			isSubmitting = true;
			setTimeout(() => {
				isSubmitting = false;
			}, 1000);
		}
	}}
>
	<label for="username">Username:</label>
	<br />
	<input id="username" name="username" type="text" bind:value={values.username} />
	<br />

	<label for="email">Email:</label>
	<br />
	<input id="email" name="email" type="email" bind:value={values.email} />
	<br />

	<label for="password">Password:</label>
	<br />
	<input id="password" name="password" type="password" bind:value={values.password} />
	<br />

	<Button type="submit" disabled={isSubmitting}>Submit</Button>
</form>
