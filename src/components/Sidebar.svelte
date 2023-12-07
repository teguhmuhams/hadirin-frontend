<script>
	import { goto } from '$app/navigation';
	import { apiUrl } from '$lib';

	const logout = async () => {
		await fetch(`${apiUrl}/logout`, {
			method: 'POST',
			headers: {
				'Content-Type': 'application/json'
			},
			credentials: 'include'
		});

		await goto('/login');
	};
</script>

<div class="sidenav">
	<div class="beranda">
		<a href="/dashboard"><img src="/img/home-page.png" alt="home page" />Beranda</a>
	</div>
	<div class="logout">
		<button class="btn btn-secondary w-100" on:click={logout}>Log Out</button>
	</div>
</div>
