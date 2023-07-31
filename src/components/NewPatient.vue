<script>
export default {
	emits: ["tab"],
	props: ["doctorId"],
	inject: ["mongo"],
	data() {
		return {
			genderbtns: ["Male", "Female"],
			residencybtns: [],
			maritalbtns: [],
			educationbtns: [],
			suicidebtns: [],
			familybtns: [],
			pphbtns: [],
			pmshbtns: [],
			drugsbtns: [],
			specialistbtns: [],
			alcoholbtns: [],
			substancebtns: [],
			appearancebtns: [],
			speechbtns: [],
			moodbtns: [],
			cognitivebtns: [],
			perceptionbtns: [],
			thoughtbtns: [],
			patientName: null,
			birthdate: null,
			occupation: null,
			maritalStatusNotes: null,
			gender: null,
			residency: null,
			marital: null,
			education: null,
			chief: null,
			hopi: null,
			suicide: null,
			specialist: null,
			family: [],
			psh: [],
			pmsh: [],
			drugs: [],
			alcohol: null,
			substance: [],
			personal: null,
			ddx: null,
			speech: [],
			mood: [],
			thought: [],
			perception: [],
			cognitive: [],
			appearance: [],
			suicidenotes: null,
			familynotes: null,
			pshnotes: null,
			pmshnotes: null,
			drugsnotes: null,
			alcoholnotes: null,
			substancenotes: null,
			perceptionnotes: null,
			thoughtnotes: null,
			management: null,
			attachment: null,
		};
	},
	methods: {
		attach(event) {
			console.log("attaching");
			console.log(event.target.files[0].type);
			this.attachment = {
				document: {
					date: new Date(),
					content_type: event.target.files[0].type,
					data: event.target.files[0],
				},
			};
		},
		push(v, input) {
			switch (v) {
				case "family":
					if (input === "None") {
						this.family = ["None"];
						break;
					}
					this.family = this.family.filter((item) => item !== "None");
					let p = this.family.find((item) => item === input);
					if (!p) {
						this.family.push(input);
					} else {
						this.family = this.family.filter((item) => item !== input);
					}
					break;
				case "psh":
					if (input === "None") {
						this.psh = ["None"];
						break;
					}
					this.psh = this.psh.filter((item) => item !== "None");
					let m = this.psh.find((item) => item === input);
					if (!m) {
						this.psh.push(input);
					} else {
						this.psh = this.psh.filter((item) => item !== input);
					}
					break;
				case "pmsh":
					if (input === "None") {
						this.pmsh = ["None"];
						break;
					}
					this.pmsh = this.pmsh.filter((item) => item !== "None");
					let x = this.pmsh.find((item) => item === input);
					if (!x) {
						this.pmsh.push(input);
					} else {
						this.pmsh = this.pmsh.filter((item) => item !== input);
					}
					break;
				case "drugs":
					if (input === "None") {
						this.drugs = ["None"];
						break;
					}
					this.drugs = this.drugs.filter((item) => item !== "None");
					let r = this.drugs.find((item) => item === input);
					if (!r) {
						this.drugs.push(input);
					} else {
						this.drugs = this.drugs.filter((item) => item !== input);
					}
					break;
				case "substance":
					if (input === "None") {
						this.substance = ["None"];
						break;
					}
					this.substance = this.substance.filter((item) => item !== "None");
					let y = this.substance.find((item) => item === input);
					if (!y) {
						this.substance.push(input);
					} else {
						this.substance = this.substance.filter((item) => item !== input);
					}
					break;
				case "appearance":
					if (input === "None") {
						this.appearance = ["None"];
						break;
					}
					this.appearance = this.appearance.filter((item) => item !== "None");
					let u = this.appearance.find((item) => item === input);
					if (!u) {
						this.appearance.push(input);
					} else {
						this.appearance = this.appearance.filter((item) => item !== input);
					}
					break;
				case "speech":
					if (input === "None") {
						this.speech = ["None"];
						break;
					}
					this.speech = this.speech.filter((item) => item !== "None");
					let q = this.speech.find((item) => item === input);
					if (!q) {
						this.speech.push(input);
					} else {
						this.speech = this.speech.filter((item) => item !== input);
					}
					break;
				case "mood":
					if (input === "None") {
						this.mood = ["None"];
						break;
					}
					this.mood = this.mood.filter((item) => item !== "None");
					let g = this.mood.find((item) => item === input);
					if (!g) {
						this.mood.push(input);
					} else {
						this.mood = this.mood.filter((item) => item !== input);
					}
					break;
				case "cognitive":
					if (input === "None") {
						this.cognitive = ["None"];
						break;
					}
					this.cognitive = this.cognitive.filter((item) => item !== "None");
					let j = this.cognitive.find((item) => item === input);
					if (!j) {
						this.cognitive.push(input);
					} else {
						this.cognitive = this.cognitive.filter((item) => item !== input);
					}
					break;
				case "perception":
					if (input === "None") {
						this.perception = ["None"];
						break;
					}
					this.perception = this.perception.filter((item) => item !== "None");
					let k = this.perception.find((item) => item === input);
					if (!k) {
						this.perception.push(input);
					} else {
						this.perception = this.perception.filter((item) => item !== input);
					}
					break;
				case "thought":
					if (input === "None") {
						this.thought = ["None"];
						break;
					}
					this.thought = this.thought.filter((item) => item !== "None");
					let l = this.thought.find((item) => item === input);
					if (!l) {
						this.thought.push(input);
					} else {
						this.thought = this.thought.filter((item) => item !== input);
					}
					break;

				default:
					break;
			}
		},
		async submitPatient() {
			const collection = this.mongo.db("psychiatry-db").collection("patients");
			let allData = {
				"created At": Date.now(),
				"Added by": this.doctorId,
				Name: this.patientName,
				"Birth Date": this.birthdate,
				Occupation: this.occupation
					? [
							{
								doctor: this.doctorId,
								date: new Date(),
								comment: this.occupation,
							},
					  ]
					: null,
				Gender: this.gender,
				Residency: this.residency,
				"Marietal Status": this.marital,
				"Marital Notes": this.maritalStatusNotes
					? [
							{
								doctor: this.doctorId,
								date: new Date(),
								comment: `${this.marital ? this.marital : ""} - ${
									this.maritalStatusNotes
								}`,
							},
					  ]
					: null,
				Education: this.education,
				"Chief Complaint": this.chief
					? [
							{
								doctor: this.doctorId,
								date: new Date(),
								comment: this.chief,
							},
					  ]
					: null,
				"History of Present Illness": this.hopi
					? [
							{
								doctor: this.doctorId,
								date: new Date(),
								comment: this.hopi,
							},
					  ]
					: null,
				Suicide: this.suicide,
				"Suicide Notes": this.suicidenotes
					? [
							{
								doctor: this.doctorId,
								date: new Date(),
								comment: this.suicidenotes,
							},
					  ]
					: null,
				"Family History": this.family,
				"Family History Notes": this.familynotes
					? [
							{
								doctor: this.doctorId,
								date: new Date(),
								comment: this.familynotes,
							},
					  ]
					: null,
				"Past Psychiatric History": this.psh,
				"Past Psychiatric History Notes": this.pshnotes
					? [
							{
								doctor: this.doctorId,
								date: new Date(),
								comment: this.pshnotes,
							},
					  ]
					: null,
				"Past Medical & Surgical History": this.pmsh,
				"Past Medical & Surgical History Notes": this.pmshnotes
					? [
							{
								doctor: this.doctorId,
								date: new Date(),
								comment: this.pmshnotes,
							},
					  ]
					: null,
				Drugs: this.drugs,
				"Drugs Notes": this.drugsnotes
					? [
							{
								doctor: this.doctorId,
								date: new Date(),
								comment: this.drugsnotes,
							},
					  ]
					: null,
				Alcohol: this.alcohol,
				"Alcohol Notes": this.alcoholnotes
					? [
							{
								doctor: this.doctorId,
								date: new Date(),
								comment: this.alcoholnotes,
							},
					  ]
					: null,
				"Substance Abuse": this.substance,
				"Substance Abuse Notes": this.substancenotes
					? [
							{
								doctor: this.doctorId,
								date: new Date(),
								comment: this.substancenotes,
							},
					  ]
					: null,
				"Personal Hx": this.personal
					? [
							{
								doctor: this.doctorId,
								date: new Date(),
								comment: this.personal,
							},
					  ]
					: null,
				DDX: this.ddx
					? [
							{
								doctor: this.doctorId,
								date: new Date(),
								comment: this.ddx,
							},
					  ]
					: null,
				"Appearance/Behavior": this.appearance,
				Speech: this.speech,
				Mood: this.mood,
				"Cognitive State": this.cognitive,
				Perception: this.perception,
				"Perception Notes": this.perceptionnotes
					? [
							{
								doctor: this.doctorId,
								date: new Date(),
								comment: this.perceptionnotes,
							},
					  ]
					: null,
				"Thought Content": this.thought,
				"Thought Content Notes": this.thoughtnotes
					? [
							{
								doctor: this.doctorId,
								date: new Date(),
								comment: this.thoughtnotes,
							},
					  ]
					: null,
				Management: this.management
					? [
							{
								doctor: this.doctorId,
								date: new Date(),
								comment: this.management,
							},
					  ]
					: null,
				Specialist: this.specialist,
			};
			this.attachment ? (allData.attachments = this.attachment) : null;
			const result = await collection.insertOne(allData);
			console.log(result);
		},
		reset() {
			this.patientName = null;
			this.birthdate = null;
			this.occupation = null;
			this.maritalStatusNotes = null;
			this.gender = null;
			this.residency = null;
			this.marital = null;
			this.education = null;
			this.relatives = null;
			this.chief = null;
			this.hopi = null;
			this.precipitant = null;
			this.suicide = null;
			this.specialist = null;
			this.family = [];
			this.children = null;
			this.psh = [];
			this.pmsh = [];
			this.drugs = [];
			this.alcohol = null;
			this.substance = [];
			this.forensic = null;
			this.social = null;
			this.ddx = null;
			this.speech = [];
			this.mood = [];
			this.thought = [];
			this.perception = [];
			this.cognitive = [];
			this.appearance = [];
			this.suicidenotes = null;
			this.familynotes = null;
			this.childrennotes = null;
			this.pshnotes = null;
			this.pmshnotes = null;
			this.drugsnotes = null;
			this.alcoholnotes = null;
			this.substancenotes = null;
			this.perceptionnotes = null;
			this.thoughtnotes = null;
			this.management = null;
		},
	},
};
</script>

<template>
	<div>
		<div @click="reset" class="reset d-flex">
			<button
				@click="submitPatient"
				class="btn text-light clicked flex-grow-1 shadow">
				Submit
			</button>
			<button class="btn btn-danger text-light ms-4 shadow">Reset</button>
		</div>

		<div class="container my-3">
			<div class="py-2 arabic">
				<h5>Name</h5>
				<input v-model="patientName" type="text" class="form-control" />
			</div>
			<div class="py-2 arabic">
				<h5>Attachment</h5>
				<input @change="attach" type="file" class="form-control" />
			</div>
			<div class="py-2">
				<h5>Birth Date</h5>
				<input v-model="birthdate" type="date" class="form-control" />
			</div>
			<div class="py-2 pb-4 group">
				<h5>Occupation</h5>
				<input v-model="occupation" type="text" class="form-control" />
			</div>
			<div class="py-4 group">
				<h5>Gender</h5>
				<button
					@click="gender = genderbtn"
					v-for="genderbtn in genderbtns"
					:key="genderbtn"
					class="btn btn-single"
					:class="gender === genderbtn ? 'clicked' : ''">
					{{ genderbtn }}
				</button>
			</div>
			<div class="py-4 group">
				<h5>Residency</h5>
				<button
					@click="residency = residencybtn"
					v-for="residencybtn in residencybtns"
					:key="residencybtn"
					class="btn btn-single arabic"
					:class="residency === residencybtn ? 'clicked' : ''">
					{{ residencybtn }}
				</button>
			</div>
			<div class="py-4 group">
				<h5>Marital Status</h5>
				<button
					@click="marital = maritalbtn"
					v-for="maritalbtn in maritalbtns"
					:key="maritalbtn"
					class="btn btn-single"
					:class="marital === maritalbtn ? 'clicked' : ''">
					{{ maritalbtn }}
				</button>
				<div class="py-4" v-if="marital">
					<h5>Marital Notes</h5>
					<textarea
						v-model="maritalStatusNotes"
						class="form-control"
						rows="3"></textarea>
				</div>
			</div>
			<div class="py-4 group">
				<h5>Education</h5>
				<button
					@click="education = educationbtn"
					v-for="educationbtn in educationbtns"
					:key="educationbtn"
					class="btn btn-single"
					:class="education === educationbtn ? 'clicked' : ''">
					{{ educationbtn }}
				</button>
			</div>
			<div class="py-4 group">
				<h5>Chief Complaint</h5>
				<textarea v-model="chief" class="form-control" rows="3"></textarea>
			</div>
			<div class="py-4 group">
				<h5>History Of Present Illness</h5>
				<textarea v-model="hopi" class="form-control" rows="3"></textarea>
			</div>
			<div class="py-4 group">
				<h5>Suicide</h5>
				<button
					@click="suicide = suicidebtn"
					v-for="suicidebtn in suicidebtns"
					:key="suicidebtn"
					class="btn btn-single"
					:class="suicide === suicidebtn ? 'clicked' : ''">
					{{ suicidebtn }}
				</button>
				<div v-if="suicide">
					<h5 class="pt-4">Notes</h5>
					<textarea
						v-model="suicidenotes"
						class="form-control"
						id="suicide"
						rows="3"></textarea>
				</div>
			</div>
			<div class="py-4 group">
				<h5>Family History</h5>
				<button
					@click="push('family', familybtn)"
					v-for="familybtn in familybtns"
					:key="familybtn"
					class="btn btn-multiple"
					:class="family.find((item) => item === familybtn) ? 'clicked' : ''">
					{{ familybtn }}
				</button>
				<div v-if="family.length > 0">
					<h5 class="pt-4">Notes</h5>
					<textarea
						v-model="familynotes"
						class="form-control"
						id="family"
						rows="3"></textarea>
				</div>
			</div>
			<div class="py-4 group">
				<h5>Past Psychiatric History</h5>
				<button
					@click="push('psh', pphbtn)"
					v-for="pphbtn in pphbtns"
					:key="pphbtn"
					class="btn btn-multiple"
					:class="psh.find((item) => item === pphbtn) ? 'clicked' : ''">
					{{ pphbtn }}
				</button>
				<div v-if="psh.length > 0">
					<h5 class="pt-4">Notes</h5>
					<textarea v-model="pshnotes" class="form-control" rows="3"></textarea>
				</div>
			</div>
			<div class="py-4 group">
				<h5>Past Medical & Surgical History</h5>
				<button
					@click="push('pmsh', pmshbtn)"
					v-for="pmshbtn in pmshbtns"
					:key="pmshbtn"
					class="btn btn-multiple"
					:class="pmsh.find((item) => item === pmshbtn) ? 'clicked' : ''">
					{{ pmshbtn }}
				</button>
				<div v-if="pmsh.length > 0">
					<h5 class="pt-4">Notes</h5>
					<textarea
						v-model="pmshnotes"
						class="form-control"
						rows="3"></textarea>
				</div>
			</div>
			<div class="py-4 group">
				<h5>Drugs</h5>
				<button
					@click="push('drugs', drugsbtn)"
					v-for="drugsbtn in drugsbtns"
					:key="drugsbtn"
					class="btn btn-multiple"
					:class="drugs.find((item) => item === drugsbtn) ? 'clicked' : ''">
					{{ drugsbtn }}
				</button>
				<div v-if="drugs.length > 0">
					<h5 class="pt-4">Notes</h5>
					<textarea
						v-model="drugsnotes"
						class="form-control"
						rows="3"></textarea>
				</div>
			</div>
			<div class="py-4 group">
				<h5>Alcohol</h5>
				<button
					@click="alcohol = alcoholbtn.value"
					v-for="alcoholbtn in alcoholbtns"
					:key="alcoholbtn.title"
					class="btn btn-single"
					:class="alcohol === alcoholbtn.value ? 'clicked' : ''">
					{{ alcoholbtn.title }}
				</button>
				<div v-if="alcohol">
					<h5 class="pt-4">Notes</h5>
					<textarea
						v-model="alcoholnotes"
						class="form-control"
						id="children"
						rows="3"></textarea>
				</div>
			</div>
			<div class="py-4 group">
				<h5>Substance Abuse</h5>
				<button
					@click="push('substance', substancebtn)"
					v-for="substancebtn in substancebtns"
					:key="substancebtn"
					class="btn btn-multiple"
					:class="
						substance.find((item) => item === substancebtn) ? 'clicked' : ''
					">
					{{ substancebtn }}
				</button>
				<div v-if="substance.length > 0">
					<h5 class="pt-4">Notes</h5>
					<textarea
						v-model="substancenotes"
						class="form-control"
						rows="3"></textarea>
				</div>
			</div>
			<div class="py-4 group">
				<h5 class="">Personal History</h5>
				<textarea v-model="personal" class="form-control" rows="6"></textarea>
			</div>
			<div class="py-4 group">
				<h5>Appearance/Behavior</h5>
				<button
					@click="push('appearance', appearancebtn)"
					v-for="appearancebtn in appearancebtns"
					:key="appearancebtn"
					class="btn btn-multiple"
					:class="
						appearance.find((item) => item === appearancebtn) ? 'clicked' : ''
					">
					{{ appearancebtn }}
				</button>
			</div>
			<div class="py-4 group">
				<h5>Speech</h5>
				<button
					@click="push('speech', speechbtn)"
					v-for="speechbtn in speechbtns"
					:key="speechbtn"
					class="btn btn-multiple"
					:class="speech.find((item) => item === speechbtn) ? 'clicked' : ''">
					{{ speechbtn }}
				</button>
			</div>
			<div class="py-4 group">
				<h5>Mood</h5>
				<button
					@click="push('mood', moodbtn)"
					v-for="moodbtn in moodbtns"
					:key="moodbtn"
					class="btn btn-multiple"
					:class="mood.find((item) => item === moodbtn) ? 'clicked' : ''">
					{{ moodbtn }}
				</button>
			</div>
			<div class="py-4 group">
				<h5>Cognitive State</h5>
				<button
					@click="push('cognitive', cognitivebtn)"
					v-for="cognitivebtn in cognitivebtns"
					:key="cognitivebtn"
					class="btn btn-multiple"
					:class="
						cognitive.find((item) => item === cognitivebtn) ? 'clicked' : ''
					">
					{{ cognitivebtn }}
				</button>
			</div>
			<div class="py-4 group">
				<h5>Perception</h5>
				<button
					@click="push('perception', perceptionbtn)"
					v-for="perceptionbtn in perceptionbtns"
					:key="perceptionbtn"
					class="btn btn-multiple"
					:class="
						perception.find((item) => item === perceptionbtn) ? 'clicked' : ''
					">
					{{ perceptionbtn }}
				</button>

				<textarea
					v-if="perception.length > 0"
					v-model="perceptionnotes"
					class="form-control mt-4"
					rows="3"></textarea>
			</div>
			<div class="py-4 group">
				<h5>Though Content</h5>
				<button
					@click="push('thought', thoughtbtn)"
					v-for="thoughtbtn in thoughtbtns"
					:key="thoughtbtn"
					class="btn btn-multiple"
					:class="thought.find((item) => item === thoughtbtn) ? 'clicked' : ''">
					{{ thoughtbtn }}
				</button>
				<textarea
					v-if="thought.length > 0"
					v-model="thoughtnotes"
					class="form-control mt-4"
					rows="3"></textarea>
			</div>
			<div class="py-4 group">
				<h5>Differential Diagnosis</h5>
				<textarea v-model="ddx" class="form-control" rows="3"></textarea>
			</div>
			<div class="py-4 group">
				<h5>Management</h5>
				<textarea
					v-model="management"
					class="form-control mt-4"
					rows="3"></textarea>
			</div>
			<div class="py-4 mb-5">
				<h5>Specialist</h5>
				<button
					v-for="specialistbtn in specialistbtns"
					:key="specialistbtn"
					class="btn btn-single arabic"
					:class="specialist === specialistbtn ? 'clicked' : ''"
					@click="specialist = specialistbtn">
					{{ specialistbtn }}
				</button>
			</div>
		</div>
	</div>
</template>

<style scoped>
.reset {
	position: fixed;
	bottom: 2%;
	right: 3%;
	left: 3%;
}
.submit {
	width: 80%;
	position: fixed;
	bottom: 2%;
	left: 3%;
}
.group {
	border-bottom: 3px solid rgb(4, 133, 90);
}

.btn-single {
	font-size: 0.9rem;
	color: white;
	background-color: rgb(201, 201, 201);
	border-radius: 500px;
	margin: 5px 5px 5px 0px;
}
.btn-multiple {
	font-size: 0.9rem;
	color: white;
	background-color: rgb(201, 201, 201);
	margin: 5px 5px 5px 0px;
}

.btn:hover {
	background-color: rgb(39, 168, 97);
}
.btn {
	box-shadow: none;
}

.clicked {
	background-color: rgb(0, 160, 200);
}
</style>
