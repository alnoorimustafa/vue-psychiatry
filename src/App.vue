<script setup>
import NewPatient from "./components/NewPatient.vue";
import EditPatient from "./components/EditPatient.vue";
import Table from "./components/Table.vue";
import Sign from "./components/Sign.vue";
import User from "./components/User.vue";
import * as Realm from "realm-web";
</script>

<script>
const {
	BSON: { ObjectId },
} = Realm;
const app = new Realm.App({ id: "psychiatry-app-jkwtz" });
const mongo = app.currentUser.mongoClient("mongodb-atlas");

export default {
	data() {
		return {
			tab: "sign",
			currentPatient: {},
			doctor: null,
			image: "",
		};
	},
	provide() {
		return { app: app, mongo: mongo };
	},
	methods: {
		tabs(tab) {
			this.tab = tab;
		},
		edit(patientId) {
			this.currentPatient = patientId;
			this.tab = "edit";
		},

		logout() {
			this.user = null;
			this.tab = "sign";
		},
	},
};
</script>

<template>
	<div>
		<div
			class="shadow nav sticky-top color pt-2 flex-row d-flex justify-content-between">
			<div class="flex-fill">
				<button
					@click="tabs('new')"
					class="btn mx-1 text-light gg"
					:class="tab === 'sign' || tab === 'new' ? 'active' : ''">
					{{ doctor ? "New Patient" : "Login" }}
				</button>

				<button
					@click="tabs('patients')"
					class="btn mx-1 text-light gg"
					:class="tab === 'patients' ? 'active' : ''"
					v-if="doctor">
					patients
				</button>
				<button
					v-if="tab === 'edit'"
					class="btn mx-1 gg"
					:class="tab === 'edit' ? 'active' : ''">
					View Patient
				</button>
			</div>
			<button
				@click="tab = 'profile'"
				class="btn mx-1 text-light gg"
				:class="tab === 'profile' ? 'active' : ''">
				<i class="bi bi-person"></i>
			</button>
		</div>

		<div v-if="!doctor">
			<Sign
				@user="
					(user) => {
						doctor = user;
						tab = 'new';
					}
				"></Sign>
		</div>

		<div v-else>
			<div>
				<User
					@close="tab = 'new'"
					@logout="() => (doctor = null)"
					v-if="tab === 'profile'"></User>
				<Table v-if="tab === 'patients'" @patient="edit" />
				<EditPatient
					:doctorId="doctor.id"
					:patient="currentPatient"
					v-if="tab === 'edit'"
					@close="tab = 'patients'" />
				<keep-alive>
					<NewPatient :doctorId="doctor.id" v-if="tab === 'new'" @tab="tabs" />
				</keep-alive>
			</div>
		</div>
	</div>
</template>

<style>
.icon {
	font-size: 1.5rem;
}

.bb {
	border: 1px black solid;
}
.gg {
	font-size: 18px;
}

.active {
	background-color: rgb(255, 255, 255);
	border-radius: 10px 10px 0px 0px;
	transition: 0.5s ease-in-out;
	color: black !important;
}

.color {
	background: rgb(0, 160, 200);
}

@font-face {
	font-family: Rubik;
	src: url(./assets/Fonts/Rubik.ttf);
}

#app {
	font-family: Rubik, Arial, sans-serif !important;
}

@media screen and (max-width: 800px) {
	.gg {
		font-size: 0.9rem;
	}
}
</style>
