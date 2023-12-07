<script>
	import Navbar from '../../components/Navbar.svelte';
	import Sidebar from '../../components/Sidebar.svelte';
</script>

<Navbar />

<Sidebar />

<div class="konten">
	<Sidebar />
	<div class="main">
		<form class="form-inline my-2 my-lg-0" id="form">
			<input
				class="form-control mr-sm-2"
				type="search"
				placeholder="Search"
				aria-label="Search"
				id="cari"
			/>
			<button class="btn btn-outline-success my-2 my-sm-0" type="submit"> Search </button>
		</form>
		<slot />
	</div>
</div>
