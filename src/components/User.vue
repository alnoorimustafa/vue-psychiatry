<template>
	<div class="modal-open show fade">
		<div class="modal-dialog">
			<div class="modal-content">
				<div class="modal-header">
					<h5 class="modal-title">{{ user }}</h5>
					<button @click="$emit('close')" class="btn-close"></button>
				</div>
				<div class="modal-body">
					<p>you can log out</p>
				</div>
				<div class="modal-footer">
					<button
						@click="$emit('logout')"
						type="button"
						class="btn btn-secondary">
						Log Out
					</button>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	props: ["user"],
};
</script>
