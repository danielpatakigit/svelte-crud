<script lang="ts">
	import type { PageData } from './$types'

	export let data: PageData
	$: ({ article } = data)
</script>

<form action="?/updateArticle" method="POST">
	<h3>Editing: {article.title}</h3>
	<label for="title"> Title </label>
	<input
		value={article.title}
		type="text"
		minlength="1"
		maxlength="100"
		id="title"
		name="title"
		required
	/>
	<label for="title"> Title </label>
	<textarea
		value={article.content}
		id="content"
		name="content"
		rows={5}
		minlength="1"
		maxlength="1000"
		required
	/>
	<button type="submit">Update Article</button>
</form>
