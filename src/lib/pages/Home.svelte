<script>
	import Button from '../Button.svelte';
	import { Field, Form } from '../Form';
	import { validateRequiredField, validateEmail } from '../utils/validation';
</script>

<Form
	on:submit={(e) => {
		console.log(e.detail);
	}}
	initialValues={{ username: 'Test', email: 'test@test.com' }}
>
	<Field label="Username" name="username" type="text" validate={validateRequiredField} />
	<Field
		label="Email"
		name="email"
		type="email"
		validate={(value, label) => {
			return validateRequiredField(value, label) || validateEmail(value, label);
		}}
	/>
	<Field label="Password" name="password" type="password" validate={validateRequiredField} />
	<Button type="submit">Submit</Button>
</Form>
