<script>
	import About from '$lib/about.svelte';
	import Pfp from '$lib/pfp.svelte';
</script>

<Pfp />
<main>
	<div class="home-text">
		<h1>Hi, I'm Ghadeer Akleh</h1>
		<h2>Welcome to my website</h2>
		<p>
			I'm an IT university student, focusing on the software development track with a keen interest
			in Front-end development. On this website you can learn more about me
		</p>
	</div>
	<About />
</main>

<style>
	main {
		height: 170vh;
		padding: 0 10%;
		display: flex;
		align-items: center;
		justify-content: center;
		/* background-color: brown; */
	}

	.home-text {
		position: absolute;
		left: 15%;
		top: 32%;
		color: rgb(42, 42, 42);
		max-width: 525px;
		line-height: 1.5;
	}

	.home-text h1 {
		font-size: 50px;
		font-weight: 700;
	}

	.home-text h2 {
		font-size: 32px;
		font-weight: 700;
		color: rgb(26, 174, 243);
	}

	.home-text p {
		margin-top: 10px;
		font-size: 18px;
		font-weight: 500;
	}
</style>
