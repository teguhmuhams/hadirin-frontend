<script>
	import { goto } from '$app/navigation';
	import { apiUrl } from '$lib';

	let email = '';
	let password = '';

	const login = async () => {
		try {
			const response = await fetch(`${apiUrl}/login`, {
				method: 'POST',
				headers: {
					'Content-Type': 'application/json'
				},
				body: JSON.stringify({ email, password }),
				credentials: 'include'
			});

			if (!response.ok) {
				throw new Error('Login failed');
			}

			goto('/dashboard'); // Redirect to dashboard after login
		} catch (error) {
			console.error('Login error:', error);
		}
	};
</script>

<div class="container-fluid d-flex align-items-center justify-content-center">
	<div class="gambar">
		<img src="/img/logo hadirin.png" alt="" />
		<img src="/img/attendance.png" alt="" />
	</div>
	<div class="login">
		<form on:submit|preventDefault={login}>
			<h1>Log In</h1>
			<img src="/img/login logo.png" alt="" />
			<div class="mb-3">
				<input type="text" class="form-control" placeholder="Email" bind:value={email} />
			</div>
			<div class="mb-3">
				<input type="password" class="form-control" placeholder="Password" bind:value={password} />
			</div>
			<button type="submit" id="btn-login" class="btn btn-primary"> Log In </button>
			<div id="or">
				<hr />
				<h3>or</h3>
				<hr />
			</div>
			<div class="ubah-password">
				<button>
					<img src="/img/ubah pw.png" alt="" />
					<h2>Ubah Password</h2>
				</button>
			</div>
		</form>
	</div>
</div>
