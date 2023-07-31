<script>
export default {
	inject: ["app", "mongo"],
	props: {
		doctorId: String,
		patient: Object,
	},
	emits: ["close"],
	data() {
		return {
			currentPatient: null,
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
			alcoholbtns: [
				{ title: "Consume Alcohol", value: true },
				{ title: "Not Consuming Alcohol", value: false },
			],
			substancebtns: [],
			appearancebtns: [],
			speechbtns: [],
			moodbtns: [],
			cognitivebtns: [],
			perceptionbtns: [],
			thoughtbtns: [],
			patientName: this.patient.Name,
			birthdate: this.patient["Birth Date"],
			newOccupation: null,
			gender: this.patient.Gender,
			residency: this.patient.Residency,
			marital: this.patient["Marietal Status"],
			newMaritalStatusNotes: null,
			education: this.patient.Education,
			newChief: null,
			newhopi: null,
			suicide: this.patient.Suicide,
			newsuicidenotes: null,
			family: this.patient["Family History"],
			newfamilynotes: null,
			psh: this.patient["Past Psychiatric History"],
			newpshnotes: null,
			pmsh: this.patient["Past Medical & Surgical History"],
			newpmshnotes: null,
			drugs: this.patient.Drugs,
			newdrugsnotes: null,
			alcohol: this.patient.Alcohol,
			newalcoholnotes: null,
			substance: this.patient["Substance Abuse"],
			newsubstancenotes: null,
			newpersonal: null,
			// ddx: this.patient.DDX,
			newddx: null,
			appearance: this.patient["Appearance/Behavior"],
			speech: this.patient.Speech,
			mood: this.patient.Mood,
			cognitive: this.patient["Cognitive State"],
			perception: this.patient.Perception,
			newperceptionnotes: null,
			thought: this.patient["Thought Content"],
			newthoughtnotes: null,
			newmanagement: null,
			specialist: this.patient.Specialist,
			newAttachment: null,
			sort: true,
		};
	},
	computed: {
		occupation() {
			if (!this.patient.Occupation) return;
			let tt = this.sort
				? this.patient.Occupation.sort(function (a, b) {
						return new Date(b.date) - new Date(a.date);
				  })
				: this.patient.Occupation.sort(function (a, b) {
						return new Date(a.date) - new Date(b.date);
				  });
			return tt.map((el) => {
				return `(${el.doctor.slice(8, 12)} @ ${new Date(
					el.date
				).toLocaleDateString("en-GB")}) : ${el.comment} \n`;
			});
		},
		maritalStatusNotes() {
			if (!this.patient["Marital Notes"]) return;
			let tt = this.sort
				? this.patient["Marital Notes"].sort(function (a, b) {
						return new Date(b.date) - new Date(a.date);
				  })
				: this.patient["Marital Notes"].sort(function (a, b) {
						return new Date(a.date) - new Date(b.date);
				  });
			return tt.map((el) => {
				return `(${el.doctor.slice(8, 12)} @ ${new Date(
					el.date
				).toLocaleDateString("en-GB")}) : ${el.comment} \n`;
			});
		},
		chief() {
			if (!this.patient["Chief Complaint"]) return;
			let tt = this.sort
				? this.patient["Chief Complaint"].sort(function (a, b) {
						return new Date(b.date) - new Date(a.date);
				  })
				: this.patient["Chief Complaint"].sort(function (a, b) {
						return new Date(a.date) - new Date(b.date);
				  });
			return tt.map((el) => {
				return `(${el.doctor.slice(8, 12)} @ ${new Date(
					el.date
				).toLocaleDateString("en-GB")}) : ${el.comment} \n`;
			});
		},
		hopi() {
			if (!this.patient["History of Present Illness"]) return;
			let tt = this.sort
				? this.patient["History of Present Illness"].sort(function (a, b) {
						return new Date(b.date) - new Date(a.date);
				  })
				: this.patient["History of Present Illness"].sort(function (a, b) {
						return new Date(a.date) - new Date(b.date);
				  });
			return tt.map((el) => {
				return `(${el.doctor.slice(8, 12)} @ ${new Date(
					el.date
				).toLocaleDateString("en-GB")}) : ${el.comment} \n`;
			});
		},
		suicidenotes() {
			if (!this.patient["Suicide Notes"]) return;
			let tt = this.sort
				? this.patient["Suicide Notes"].sort(function (a, b) {
						return new Date(b.date) - new Date(a.date);
				  })
				: this.patient["Suicide Notes"].sort(function (a, b) {
						return new Date(a.date) - new Date(b.date);
				  });
			return tt.map((el) => {
				return `(${el.doctor.slice(8, 12)} @ ${new Date(
					el.date
				).toLocaleDateString("en-GB")}) : ${el.comment} \n`;
			});
		},
		familynotes() {
			if (!this.patient["Family History Notes"]) return;
			let tt = this.sort
				? this.patient["Family History Notes"].sort(function (a, b) {
						return new Date(b.date) - new Date(a.date);
				  })
				: this.patient["Family History Notes"].sort(function (a, b) {
						return new Date(a.date) - new Date(b.date);
				  });
			return tt.map((el) => {
				return `(${el.doctor.slice(8, 12)} @ ${new Date(
					el.date
				).toLocaleDateString("en-GB")}) : ${el.comment} \n`;
			});
		},
		pshnotes() {
			if (!this.patient["Past Psychiatric History Notes"]) return;
			let tt = this.sort
				? this.patient["Past Psychiatric History Notes"].sort(function (a, b) {
						return new Date(b.date) - new Date(a.date);
				  })
				: this.patient["Past Psychiatric History Notes"].sort(function (a, b) {
						return new Date(a.date) - new Date(b.date);
				  });
			return tt.map((el) => {
				return `(${el.doctor.slice(8, 12)} @ ${new Date(
					el.date
				).toLocaleDateString("en-GB")}) : ${el.comment} \n`;
			});
		},
		pmshnotes() {
			if (!this.patient["Past Medical & Surgical History Notes"]) return;
			let tt = this.sort
				? this.patient["Past Medical & Surgical History Notes"].sort(function (
						a,
						b
				  ) {
						return new Date(b.date) - new Date(a.date);
				  })
				: this.patient["Past Medical & Surgical History Notes"].sort(function (
						a,
						b
				  ) {
						return new Date(a.date) - new Date(b.date);
				  });
			return tt.map((el) => {
				return `(${el.doctor.slice(8, 12)} @ ${new Date(
					el.date
				).toLocaleDateString("en-GB")}) : ${el.comment} \n`;
			});
		},
		drugsnotes() {
			if (!this.patient["Drugs Notes"]) return;
			let tt = this.sort
				? this.patient["Drugs Notes"].sort(function (a, b) {
						return new Date(b.date) - new Date(a.date);
				  })
				: this.patient["Drugs Notes"].sort(function (a, b) {
						return new Date(a.date) - new Date(b.date);
				  });
			return tt.map((el) => {
				return `(${el.doctor.slice(8, 12)} @ ${new Date(
					el.date
				).toLocaleDateString("en-GB")}) : ${el.comment} \n`;
			});
		},
		alcoholnotes() {
			if (!this.patient["Alcohol Notes"]) return;
			let tt = this.sort
				? this.patient["Alcohol Notes"].sort(function (a, b) {
						return new Date(b.date) - new Date(a.date);
				  })
				: this.patient["Alcohol Notes"].sort(function (a, b) {
						return new Date(a.date) - new Date(b.date);
				  });
			return tt.map((el) => {
				return `(${el.doctor.slice(8, 12)} @ ${new Date(
					el.date
				).toLocaleDateString("en-GB")}) : ${el.comment} \n`;
			});
		},
		substancenotes() {
			if (!this.patient["Substance Abuse Notes"]) return;
			let tt = this.sort
				? this.patient["Substance Abuse Notes"].sort(function (a, b) {
						return new Date(b.date) - new Date(a.date);
				  })
				: this.patient["Substance Abuse Notes"].sort(function (a, b) {
						return new Date(a.date) - new Date(b.date);
				  });
			return tt.map((el) => {
				return `(${el.doctor.slice(8, 12)} @ ${new Date(
					el.date
				).toLocaleDateString("en-GB")}) : ${el.comment} \n`;
			});
		},
		personal() {
			if (!this.patient["Personal Hx"]) return;
			let tt = this.sort
				? this.patient["Personal Hx"].sort(function (a, b) {
						return new Date(b.date) - new Date(a.date);
				  })
				: this.patient["Personal Hx"].sort(function (a, b) {
						return new Date(a.date) - new Date(b.date);
				  });
			return tt.map((el) => {
				return `(${el.doctor.slice(8, 12)} @ ${new Date(
					el.date
				).toLocaleDateString("en-GB")}) : ${el.comment} \n`;
			});
		},
		ddx() {
			if (!this.patient.DDX) return;
			let tt = this.sort
				? this.patient.DDX.sort(function (a, b) {
						return new Date(b.date) - new Date(a.date);
				  })
				: this.patient.DDX.sort(function (a, b) {
						return new Date(a.date) - new Date(b.date);
				  });
			return tt.map((el) => {
				return `(${el.doctor.slice(8, 12)} @ ${new Date(
					el.date
				).toLocaleDateString("en-GB")}) : ${el.comment} \n`;
			});
		},
		perceptionnotes() {
			if (!this.patient["Perception Notes"]) return;
			let tt = this.sort
				? this.patient["Perception Notes"].sort(function (a, b) {
						return new Date(b.date) - new Date(a.date);
				  })
				: this.patient["Perception Notes"].sort(function (a, b) {
						return new Date(a.date) - new Date(b.date);
				  });
			return tt.map((el) => {
				return `(${el.doctor.slice(8, 12)} @ ${new Date(
					el.date
				).toLocaleDateString("en-GB")}) : ${el.comment} \n`;
			});
		},
		thoughtnotes() {
			if (!this.patient["Thought Content Notes"]) return;
			let tt = this.sort
				? this.patient["Thought Content Notes"].sort(function (a, b) {
						return new Date(b.date) - new Date(a.date);
				  })
				: this.patient["Thought Content Notes"].sort(function (a, b) {
						return new Date(a.date) - new Date(b.date);
				  });
			return tt.map((el) => {
				return `(${el.doctor.slice(8, 12)} @ ${new Date(
					el.date
				).toLocaleDateString("en-GB")}) : ${el.comment} \n`;
			});
		},
		management() {
			if (!this.patient.Management) return;
			let tt = this.sort
				? this.patient.Management.sort(function (a, b) {
						return new Date(b.date) - new Date(a.date);
				  })
				: this.patient.Management.sort(function (a, b) {
						return new Date(a.date) - new Date(b.date);
				  });
			return tt.map((el) => {
				return `(${el.doctor.slice(8, 12)} @ ${new Date(
					el.date
				).toLocaleDateString("en-GB")}) : ${el.comment} \n`;
			});
		},
	},
	methods: {
		attachmentsURL(doc) {
			let url = URL.createObjectURL(doc.data);
			return url;
		},
		attach(event) {
			this.newAttachment = this.patient._attachments;
			this.newAttachment[
				`document${Object.keys(this.patient._attachments).length + 1}`
			] = {
				content_type: event.target.files[0].type,
				data: event.target.files[0],
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
			let editedData = {
				_attachments: this.newAttachment
					? this.newAttachment
					: this.patient._attachments,
				Name: this.patientName,
				"Birth Date": this.birthdate,
				Occupation: this.newOccupation
					? this.patient.Occupation
						? [
								...this.patient.Occupation,
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: this.newOccupation,
								},
						  ]
						: [
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: this.newOccupation,
								},
						  ]
					: this.patient.Occupation
					? this.patient.Occupation
					: null,
				Gender: this.gender,
				Residency: this.residency,
				"Marietal Status": this.marital,
				"Marital Notes": this.newMaritalStatusNotes
					? this.patient["Marital Notes"]
						? [
								...this.patient["Marital Notes"],
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: `${this.marital ? this.marital : ""} - ${
										this.newMaritalStatusNotes
									}`,
								},
						  ]
						: [
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: `${this.marital ? this.marital : ""} - ${
										this.newMaritalStatusNotes
									}`,
								},
						  ]
					: this.patient["Marital Notes"]
					? this.patient["Marital Notes"]
					: null,
				Education: this.education,
				"Chief Complaint": this.newChief
					? this.patient["Chief Complaint"]
						? [
								...this.patient["Chief Complaint"],
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: this.newChief,
								},
						  ]
						: [
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: this.newChief,
								},
						  ]
					: this.patient["Chief Complaint"]
					? this.patient["Chief Complaint"]
					: null,
				"History of Present Illness": this.newhopi
					? this.patient["History of Present Illness"]
						? [
								...this.patient["History of Present Illness"],
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: this.newhopi,
								},
						  ]
						: [
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: this.newhopi,
								},
						  ]
					: this.patient["History of Present Illness"]
					? this.patient["History of Present Illness"]
					: null,
				Suicide: this.suicide,
				"Suicide Notes": this.newsuicidenotes
					? this.patient["Suicide Notes"]
						? [
								...this.patient["Suicide Notes"],
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: `${this.suicide ? this.suicide : ""} - ${
										this.newsuicidenotes
									}`,
								},
						  ]
						: [
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: `${this.suicide ? this.suicide : ""} - ${
										this.newsuicidenotes
									}`,
								},
						  ]
					: this.patient["Suicide Notes"]
					? this.patient["Suicide Notes"]
					: null,
				"Family History": this.family,
				"Family History Notes": this.newfamilynotes
					? this.patient["Family History Notes"]
						? [
								...this.patient["Family History Notes"],
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: `${this.family ? this.family : ""} - ${
										this.newfamilynotes
									}`,
								},
						  ]
						: [
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: `${this.family ? this.family : ""} - ${
										this.newfamilynotes
									}`,
								},
						  ]
					: this.patient["Family History Notes"]
					? this.patient["Family History Notes"]
					: null,
				"Past Psychiatric History": this.psh,
				"Past Psychiatric History Notes": this.newpshnotes
					? this.patient["Past Psychiatric History Notes"]
						? [
								...this.patient["Past Psychiatric History Notes"],
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: `${this.psh ? this.psh : ""} - ${this.newpshnotes}`,
								},
						  ]
						: [
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: `${this.psh ? this.psh : ""} - ${this.newpshnotes}`,
								},
						  ]
					: this.patient["Past Psychiatric History Notes"]
					? this.patient["Past Psychiatric History Notes"]
					: null,
				"Past Medical & Surgical History": this.pmsh,
				"Past Medical & Surgical History Notes": this.newpmshnotes
					? this.patient["Past Medical & Surgical History Notes"]
						? [
								...this.patient["Past Medical & Surgical History Notes"],
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: `${this.pmsh ? this.pmsh : ""} - ${
										this.newpmshnotes
									}`,
								},
						  ]
						: [
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: `${this.pmsh ? this.pmsh : ""} - ${
										this.newpmshnotes
									}`,
								},
						  ]
					: this.patient["Past Medical & Surgical History Notes"]
					? this.patient["Past Medical & Surgical History Notes"]
					: null,
				Drugs: this.drugs,
				"Drugs Notes": this.newdrugsnotes
					? this.patient["Drugs Notes"]
						? [
								...this.patient["Drugs Notes"],
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: `${this.newdrugsnotes}`,
								},
						  ]
						: [
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: `${this.newdrugsnotes}`,
								},
						  ]
					: this.patient["Drugs Notes"]
					? this.patient["Drugs Notes"]
					: null,
				Alcohol: this.alcohol,
				"Alcohol Notes": this.newalcoholnotes
					? this.patient["Alcohol Notes"]
						? [
								...this.patient["Alcohol Notes"],
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: `${this.newalcoholnotes}`,
								},
						  ]
						: [
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: `${this.newalcoholnotes}`,
								},
						  ]
					: this.patient["Alcohol Notes"]
					? this.patient["Alcohol Notes"]
					: null,
				"Substance Abuse": this.substance,
				"Substance Abuse Notes": this.newsubstancenotes
					? this.patient["Substance Abuse Notes"]
						? [
								...this.patient["Substance Abuse Notes"],
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: `${this.newsubstancenotes}`,
								},
						  ]
						: [
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: `${this.newsubstancenotes}`,
								},
						  ]
					: this.patient["Substance Abuse Notes"]
					? this.patient["Substance Abuse Notes"]
					: null,
				"Personal Hx": this.newpersonal
					? this.patient["Personal Hx"]
						? [
								...this.patient["Personal Hx"],
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: `${this.newpersonal}`,
								},
						  ]
						: [
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: `${this.newpersonal}`,
								},
						  ]
					: this.patient["Personal Hx"]
					? this.patient["Personal Hx"]
					: null,
				DDX: this.newddx
					? this.patient.DDX
						? [
								...this.patient.DDX,
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: `${this.newddx}`,
								},
						  ]
						: [
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: `${this.newddx}`,
								},
						  ]
					: this.patient.DDX
					? this.patient.DDX
					: null,
				Speech: this.speech,
				Mood: this.mood,
				Perception: this.perception,
				"Cognitive State": this.cognitive,
				"Appearance/Behavior": this.appearance,
				"Perception Notes": this.newperceptionnotes
					? this.patient["Perception Notes"]
						? [
								...this.patient["Perception Notes"],
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: `${this.newperceptionnotes}`,
								},
						  ]
						: [
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: `${this.newperceptionnotes}`,
								},
						  ]
					: this.patient["Perception Notes"]
					? this.patient["Perception Notes"]
					: null,
				"Thought Content": this.thought,
				"Thought Content Notes": this.newthoughtnotes
					? this.patient["Thought Content Notes"]
						? [
								...this.patient["Thought Content Notes"],
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: `${this.newthoughtnotes}`,
								},
						  ]
						: [
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: `${this.newthoughtnotes}`,
								},
						  ]
					: this.patient["Thought Content Notes"]
					? this.patient["Thought Content Notes"]
					: null,
				Specialist: this.specialist,
				Management: this.newmanagement
					? this.patient.Management
						? [
								...this.patient.Management,
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: `${this.newmanagement}`,
								},
						  ]
						: [
								{
									doctor: this.doctorId,
									date: new Date(),
									comment: `${this.newmanagement}`,
								},
						  ]
					: this.patient.Management
					? this.patient.Management
					: null,
			};
			const res = await collection.updateOne(
				{ _id: this.patient._id },
				editedData
			);
			console.log(res);
			this.$emit("close");
		},
	},
};
</script>

<template>
	<div @click="sort = !sort" class="sort">
		<button class="btn color">
			<i v-if="!sort" class="bi bi-arrow-up text-light"></i>
			<i v-if="sort" class="bi bi-arrow-down text-light"></i>
		</button>
	</div>
	<div class="font container mt-3">
		<div class="py-2 shadow sticky-top mb-3">
			<button
				@click="$emit('close')"
				type="button"
				class="btn-close px-2"></button>
		</div>
		<div class="py-2 arabic">
			<h5>Name</h5>
			<input
				:placeholder="patientName"
				type="text"
				class="form-control"
				disabled />
		</div>
		<div class="py-2 arabic">
			<h5>New Attachment</h5>
			<input @change="attach" type="file" class="form-control" />
		</div>
		<div class="py-2 arabic">
			<h5>Attachments</h5>
			<img
				v-for="doc in patient._attachments"
				:key="doc"
				:src="attachmentsURL(doc)"
				class="w-100 pb-4" />
		</div>
		<div class="py-2">
			<h5>Birth Date</h5>
			<input type="date" class="form-control" v-model="birthdate" disabled />
		</div>
		<div class="py-2 group">
			<h5>Occupation</h5>
			<textarea
				v-model="newOccupation"
				type="text"
				class="form-control"
				:placeholder="occupation"
				rows="3"></textarea>
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
					v-model="newMaritalStatusNotes"
					:placeholder="maritalStatusNotes"
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
			<textarea
				v-model="newChief"
				:placeholder="chief"
				class="form-control"
				rows="3"></textarea>
		</div>
		<div class="py-4 group">
			<h5>History Of Present Illness</h5>
			<textarea
				v-model="newhopi"
				:placeholder="hopi"
				class="form-control"
				rows="3"></textarea>
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
			<div v-if="suicide && suicide !== 'None'">
				<h5 class="pt-4">Notes</h5>
				<textarea
					v-model="newsuicidenotes"
					:placeholder="suicidenotes"
					class="form-control"
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
					v-model="newfamilynotes"
					:placeholder="familynotes"
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
				<textarea
					v-model="newpshnotes"
					:placeholder="pshnotes"
					class="form-control"
					rows="3"></textarea>
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
					v-model="newpmshnotes"
					:placeholder="pmshnotes"
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
					v-model="newdrugsnotes"
					:placeholder="drugsnotes"
					class="form-control"
					id="children"
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
					v-model="newalcoholnotes"
					:placeholder="alcoholnotes"
					class="form-control"
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
					v-model="newsubstancenotes"
					:placeholder="substancenotes"
					class="form-control"
					rows="3"></textarea>
			</div>
		</div>
		<div class="py-4 group">
			<h5 class="">Personal History</h5>
			<textarea
				v-model="newpersonal"
				:placeholder="personal"
				class="form-control"
				rows="3"></textarea>
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
				v-model="newperceptionnotes"
				:placeholder="perceptionnotes"
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
				v-model="newthoughtnotes"
				:placeholder="thoughtnotes"
				class="form-control mt-4"
				rows="3"></textarea>
		</div>
		<div class="py-4 group">
			<h5>Management</h5>
			<textarea
				v-model="newmanagement"
				:placeholder="management"
				class="form-control mt-4"
				id="children"
				rows="3"></textarea>
		</div>
		<div class="py-4 group">
			<h5>Differential Diagnosis</h5>
			<textarea
				v-model="newddx"
				:placeholder="ddx"
				class="form-control"
				rows="3"></textarea>
		</div>
		<div class="py-4">
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
		<div class="row m-4">
			<button @click="submitPatient" class="btn btn-primary">Submit</button>
		</div>
	</div>
</template>

<style scoped>
.color {
	background: rgb(0, 160, 200);
}

img {
	cursor: pointer;
	width: 30px;
	height: auto;
	color: #fff;
}
.sort {
	position: fixed;
	bottom: 3%;
	right: 3%;
}
.sticky-top {
	top: 80px;
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
	background-color: aquamarine;
}
.btn {
	box-shadow: none;
}

.nn {
	border: 1px solid black;
}

.clicked {
	background-color: blueviolet;
}
</style>
