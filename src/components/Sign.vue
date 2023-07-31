<template>
	<form class="m-4">
		<div class="mb-3">
			<label for="exampleInputEmail1" class="form-label">email</label>
			<input v-model="email" type="text" class="form-control" />
			<div class="form-text">Never share your email with anyone else.</div>
		</div>
		<div class="mb-3">
			<label for="exampleInputPassword1" class="form-label">Password</label>
			<input v-model="password" type="password" class="form-control" />
		</div>
		<button
			@click.prevent="
				sign({ email, password });
				error = true;
			"
			class="btn btn-primary"
			:class="error ? 'btn-danger' : 'btn-profile'">
			Sign In
		</button>
	</form>
</template>

<script>
import * as Realm from "realm-web";

export default {
	inject: ["mongo", "app"],
	data() {
		return {
			email: "",
			password: "",
			error: false,
		};
	},
	methods: {
		async sign({ email, password }) {
			// Create an email/password credential
			const credentials = Realm.Credentials.emailPassword(email, password);

			// Authenticate the user
			const user = await this.app.logIn(credentials);
			if (user) {
				console.log(user);
				this.$emit("user", user);
			}
			return;
		},
	},
};
</script>
