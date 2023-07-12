<script lang="ts">
	import './comic.css';
	import { onMount } from 'svelte';
	import { formatDistanceToNow } from 'date-fns';

	interface ComicResponse {
		img: string;
		title: string;
		safe_title: string;
		num: number;
		alt: string;
		transcript: string;
		year: string;
		month: string;
		day: string;
	}

	let comic_img = '../smiley.jpg';
	let comic_title = '';
	let comic_date = '';
	let buttonClicked = false;

	async function fetch_ID(): Promise<string> {
		const email = 'g.akleh@innopolis.university';
		const url = 'https://fwd.innopolis.university/api/hw2?';
		const apiParams = new URLSearchParams();
		apiParams.append('email', email);
		const res: Response = await fetch(url + apiParams.toString());
		const id: string = await res.json();
		return id;
	}

	async function fetch_comic(): Promise<ComicResponse> {
		const id: string = await fetch_ID();
		const imageParams = new URLSearchParams();
		imageParams.append('id', id);
		const imageUrl = 'https://fwd.innopolis.university/api/comic?';
		const imgRes: Response = await fetch(imageUrl + imageParams.toString());
		const data: ComicResponse = await imgRes.json();
		return data;
	}

	async function handleClick() {
		try {
			const data: ComicResponse = await fetch_comic();

			comic_img = data.img;
			comic_title = data.safe_title;

			const releaseDate = new Date(
				parseInt(data.year),
				parseInt(data.month) - 1,
				parseInt(data.day)
			);
			const timeAgo = formatDistanceToNow(releaseDate, { addSuffix: true });
			comic_date = timeAgo;
		} catch (error) {
			console.error('Error:', error);
		}
	}

	onMount(() => {
		buttonClicked = false;
	});
</script>

<main>
	<div class="content-box">
		{#if !buttonClicked}
			<button on:click={handleClick} id="get-comic-btn">Press for a random comic</button>
		{:else}
			<button disabled />
		{/if}
	</div>
	<div id="comic-container">
		<p id="comic-title">{comic_title}</p>
		<p id="comic-date">{comic_date}</p>
		<img id="comic-image" src={comic_img} alt="comic" />
	</div>
</main>
