<script>
	export let currentUser;
	const apiUrl = import.meta.env.VITE_API_URL;

	let courses = [];

	async function getCourses(currentUser) {
		const response = await fetch(
			`${apiUrl}/courses?filter[grade_id]=${currentUser.student.grade_id}&include=grade`,
			{
				method: 'GET',
				headers: {
					'Content-Type': 'application/json'
				},
				credentials: 'include'
			}
		);
		const data = await response.json();
		courses = data.data;
	}

	getCourses(currentUser);
</script>

{#if currentUser && currentUser.student}
	<h1>Kelas {currentUser.student.grade.name}</h1>
{:else}
	<p>Loading user data...</p>
{/if}
<div id="mapel">
	<div id="mapel">
		<div class="row">
			{#each courses as course}
				<div class="col-sm-4">
					<div class="card">
						<div class="card-body">
							<div>
								<h5 class="card-title">{course.name}</h5>
								<h4 class="card-text">{course.year}</h4>
								<p class="card-text">
									{course.grade.name.match(/[a-zA-Z]/g).join('')}
								</p>
							</div>
							<img src="/img/profil guru.png" alt="" />
						</div>
						<button class="btn btn-primary">Presensi</button>
					</div>
				</div>
			{/each}
			{#if courses.length == 0}
				<p>No courses data.</p>
			{/if}
		</div>
	</div>
</div>
