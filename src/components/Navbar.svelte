<script>
	import { authenticated } from '../stores/auth';

	let auth = false;

	authenticated.subscribe((a) => (auth = a));
</script>

<nav>
	<img id="logo" src="/img/logo hadirin.png" alt="" />
	<div id="profil">
		<img src="/img/profil.png" alt="" />
		<div id="nama"></div>
	</div>
</nav>
