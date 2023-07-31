<template>
	<div class="container mt-4">
		<nav class="navbar navbar-light">
			<div class="d-flex">
				<input
					v-model="searchField"
					class="form-control me-2 arabic flex-fill"
					type="search"
					placeholder="اسم المريض" />
				<button
					@click.prevent="search"
					class="flex-fill btn btn-outline-success">
					Search
				</button>
			</div>
		</nav>
		<table class="table table-striped table-hover mt-4">
			<thead>
				<tr>
					<th scope="col">#</th>
					<th scope="col">Name</th>
					<th scope="col">Specialist</th>
					<th scope="col">Date & Time</th>
				</tr>
			</thead>
			<tbody>
				<tr
					v-for="(patient, i) in patients"
					@click="$emit('patient', patient)"
					:key="patient._id">
					<td>{{ i + 1 }}</td>
					<td class="arabic">{{ patient.Name }}</td>
					<td class="arabic">{{ patient.Specialist }}</td>
					<td scope="row">
						{{ new Date(patient["created At"]).toLocaleDateString() }}
					</td>
				</tr>
			</tbody>
		</table>
	</div>
</template>

<script>
export default {
	inject: ["mongo", "app"],
	data() {
		return {
			patients: null,
			searchField: null,
		};
	},
	methods: {
		async getPatients() {
			const collection = await this.mongo
				.db("psychiatry-db")
				.collection("patients");
			const res = await collection.find();
			if (res) {
				this.patients = res;
			}
		},
		async search() {
			const collection = await this.mongo
				.db("psychiatry-db")
				.collection("patients");

			if (this.searchField === "") {
				this.patients = await collection.find();
			} else {
				const searchResults = await collection.find({
					Name: this.searchField,
				});
				this.patients = searchResults;
			}
		},
	},
	mounted() {
		this.getPatients();
	},
};
</script>

<style scoped>
.ww {
	border: 1px solid darkblue;
}
</style>
