<script>
	import { page } from '$app/stores';
	import { apiUrl } from '$lib';
	import { onMount } from 'svelte';
	import Modal from './Modal.svelte';

	let showModal = {};

	function toggleModal(id) {
		showModal[id] = !showModal[id];
	}

	const courseId = $page.params.id;

	let course = 'loading...';
	let attendances = [];

	onMount(async () => {
		course = await getCourse(courseId);
		attendances = await getAttendances(courseId);
	});

	async function getCourse(courseId) {
		try {
			const response = await fetch(`${apiUrl}/courses/${courseId}`, {
				method: 'GET',
				headers: {
					'Content-Type': 'application/json'
				},
				credentials: 'include'
			});
			if (response.ok) {
				const data = await response.json();
				return data;
			}
		} catch (error) {
			//
			console.log('error fetching curse: ', error);
		}
	}

	async function getAttendances(courseId) {
		try {
			const response = await fetch(`${apiUrl}/attendances?filter[course_id]=${courseId}	`, {
				method: 'GET',
				headers: {
					'Content-Type': 'application/json'
				},
				credentials: 'include'
			});
			if (response.ok) {
				const data = await response.json();
				return data.data;
			}
		} catch (error) {
			console.log('error fetching attendances:', error);
		}
	}
</script>

<div class="main" id="absen">
	<h1 class="text-center">
		{course.name ? course.name : 'Loading...'}
	</h1>
	<div id="pertemuan">
		{#if attendances}
			{#each attendances as attendance}
				<Modal
					show={showModal[attendance.id]}
					{attendance}
					toggleModal={() => toggleModal(attendance.id)}
				/>
				<div class="card">
					<img
						width="50"
						height="50"
						src="/img/hand-with-smartphone.png"
						alt="hand-with-smartphone"
					/>
					<div class="card-body">
						<button class="title" on:click={() => toggleModal(attendance.id)}>
							<h5 class="card-title">Daftar Hadir {attendance.title}</h5>
						</button>
						<p class="card-text">{attendance.schedule_start}</p>
					</div>
				</div>
			{/each}
		{/if}
	</div>
</div>
