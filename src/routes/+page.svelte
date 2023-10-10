<script lang="ts">
	import { fade, fly } from 'svelte/transition'
	import { flip } from 'svelte/animate'

	import type { PageData } from './$types'
	import { enhance } from '$app/forms'

	export let data: PageData

	$: ({ articles } = data)
</script>

<div class="grid">
	<div>
		<h2>Articles:</h2>
		{#each articles as article (article.id)}
			<article animate:flip={{ duration: 600 }} transition:fly={{ x: -200 }}>
				<header>{article.title}</header>
				<p>
					{article.content}
				</p>
				<div class="grid">
					<form action="?/deleteArticle&id={article.id}" method="POST" use:enhance>
						<button type="submit" class="outline secondary">Delete Article</button>
					</form>

					<span>
						<a href="/{article.id}" role="button" class="outline constrast" style="width: 100%;"
							>Edit Article</a
						>
					</span>
				</div>
			</article>
		{/each}
	</div>
	<form action="?/createArticle" method="POST" use:enhance>
		<h3>New Article</h3>
		<label for="title"> Title </label>
		<input type="text" minlength="1" maxlength="100" id="title" name="title" required />
		<label for="title"> Title </label>
		<textarea id="content" name="content" rows={5} minlength="1" maxlength="1000" required />
		<button type="submit">Add Article</button>
	</form>
</div>
