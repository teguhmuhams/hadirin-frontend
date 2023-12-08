<script>
	import { apiUrl } from '$lib';

	export let show = false;
	export let attendance;
	export let toggleModal = () => {};

	let selectedOption;

	const send = async () => {
		try {
			const response = await fetch(
				`${apiUrl}/students/${currentUser.id}/attendances/${attendance.id}`,
				{
					method: 'POST',
					headers: {
						'Content-Type': 'application/json'
					},
					body: JSON.stringify({ selectedOption }),
					credentials: 'include'
				}
			);

			if (!response.ok) {
				throw new Error('Login failed');
			}
			goto('/dashboard'); // Redirect to dashboard after login
		} catch (error) {
			console.error('Login error:', error);
		}
	};
</script>

{#if show}
	<div class="modal show" style="display: block;" aria-labelledby={attendance.id}>
		<div class="modal-dialog modal-dialog-centered">
			<div class="modal-content">
				<div class="modal-header">
					<button
						type="button"
						class="btn-close"
						aria-label="Close"
						on:click={() => toggleModal(attendance.id)}
					></button>
				</div>
				<div class="modal-body">
					<div class="d-flex flex-column align-items-center justify-content-center">
						<h4 class="modal-title mb-1">Daftar Hadir {attendance.title}</h4>
						<p>{attendance.schedule_start}</p>
					</div>
					<form on:submit|preventDefault={send}>
						<div class="container">
							<div class="row justify-content-center">
								<div class="col-auto">
									<div class="form-check form-check-inline">
										<input
											class="form-check-input"
											type="radio"
											bind:group={selectedOption}
											name="selectedOption"
											id="inlineRadio1"
											value="Hadir"
										/>
										<label class="form-check-label" for="inlineRadio1">Hadir</label>
									</div>
									<div class="form-check form-check-inline">
										<input
											class="form-check-input"
											type="radio"
											bind:group={selectedOption}
											name="selectedOption"
											id="inlineRadio2"
											value="Sakit"
										/>
										<label class="form-check-label" for="inlineRadio2">Sakit</label>
									</div>
									<div class="form-check form-check-inline">
										<input
											class="form-check-input"
											type="radio"
											bind:group={selectedOption}
											name="selectedOption"
											id="inlineRadio3"
											value="Izin"
										/>
										<label class="form-check-label" for="inlineRadio3">Izin</label>
									</div>
								</div>
							</div>
						</div>
						<div class="d-flex justify-content-center mt-3">
							<button type="submit" class="btn btn-primary w-75">Simpan</button>
						</div>
					</form>
				</div>
			</div>
		</div>
	</div>
	<div class="modal-backdrop show"></div>
{/if}
