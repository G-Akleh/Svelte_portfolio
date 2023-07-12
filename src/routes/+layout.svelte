<script>
	import Navbar from '$lib/navbar.svelte';
	import Footer from '$lib/footer.svelte';
	import './layout.css';
</script>

<header>
	<Navbar />
</header>
<slot />
<footer>
	<Footer />
</footer>
