<script>
	import { onMount } from "svelte";
	import Subscribe from './components/subscribe.svelte'
	import sanityClient from './client.js'


	let posts = [];
	
	onMount(() => {
		sanityClient.fetch(`*[_type == "post"]{
			_id,
			title,
			'date': publishedAt,
			'image': mainImage.asset->url,
			body
		}`)
		.then((data) => posts = data)
		.catch(console.error);
	})
	
	
	
	
</script>
<div class="top">
	<p>theob.blog (bien mieux qu'instagram)</p>
	<h1>Bienvenue sur mon nouveau blog!</h1>
</div>
	
	<div class="tacos" >
		<img src="/img/tacos.png" />

	</div>



<main>
{#each posts as post, i}
	
	<div class="post">
		<div>
				<h2>{post.title}</h2>
				<h4>{post.date}</h4>
			


			<div class="body">
			
			
				
				{#each post.body as p}
					<p>{p}</p>
				{/each}
				
				
			
			</div>
		
		</div>
		<div class="img">
			<img src={`${post.image}?w=1000`} />
		</div>
	</div>
{/each}
</main>
 

<style>

	.top {
		padding: 0 24px;
	}

	.tacos {
		display: flex;
		justify-content: flex-end;
		width: 100%;
		height: 100vh;
		position: relative;
		bottom: 0;
		
		left: 0;
	}
	.tacos img {
		width: 100%;
		object-fit: cover;
	}

	main {
		margin: 100px 24px;
	}
	@media (max-width: 700px) {
		main {
			margin: 100px 14px
		}
		.top {
			padding: 0 14px;
		}
	}
	.post {
		
		padding: 24px;

	}

	post:nth-child(3n - 2) {
		background-color: brown;
	}

	.post h2, .post h4 {
		margin: 8px 0;
	}
	.post h2 {
		font-weight: 700;
		
		margin-bottom: 6px;
	}
	.post p {
		max-width: 100%;
		margin: 36px 0;
		width: 800px;
		
	}
	.img {
		display: flex;
		justify-content: flex-end;
	}
	.img img {
		max-width: 100%;
		object-fit: contain;
		border-radius: 7px;
		overflow: hidden;
	}
</style>