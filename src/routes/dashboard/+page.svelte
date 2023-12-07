<script>
	import { goto } from '$app/navigation';
	import { apiUrl } from '$lib';
	import { onMount } from 'svelte';
	import { authenticated } from '../../stores/auth';
	import Course from '../../components/Student/Course.svelte';

	let user = '';

	onMount(async () => {
		try {
			const response = await fetch(`${apiUrl}/user`, {
				method: 'GET',
				headers: {
					'Content-Type': 'application/json'
				},
				credentials: 'include'
			});

			if (response.ok) {
				user = await response.json();
				authenticated.set(true);
			} else {
				throw new Error('Failed to fetch user');
			}
		} catch (error) {
			authenticated.set(false);
			await goto('/login');
		}
	});
</script>

<!-- Student Main Dashboard -->
{#if user && user.student}
	<Course currentUser={user} />
{/if}
<!-- Teacher Main Dashboard -->

<!-- Admin Main Dashboard -->
