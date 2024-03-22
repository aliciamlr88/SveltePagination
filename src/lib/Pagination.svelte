<script>
	import { page } from '$app/stores';
	export let totalPages;

	function goToPage(pageNumber) {
		$page.url.searchParams.set('page', pageNumber);
		window.location = $page.url;
	}

	$: pageNumber = $page.url.searchParams.get('page') ?? 1;
	$: pageNumberPrevious = pageNumber > 1 ? +pageNumber - 1 : 1;
	$: pageNumberNext = pageNumber < totalPages ? +pageNumber + +1 : totalPages;

	$: startNumber =
		pageNumber - 1 > 0 && (pageNumber - 1) % 10 == 0
			? pageNumber - 4
			: pageNumber % 10 > 0
				? pageNumber - (pageNumber % 10) + 1
				: +pageNumber - 5;
	$: numbersPagination = Array.from(
		{ length: totalPages > 10 ? 10 : totalPages },
		(_, i) => +startNumber + i
	);
</script>

<nav aria-label="Pagination" class="my-4">
	<ul class="pagination">
		<li class="page-item">
			<button class="btn-link page-link" on:click={goToPage(pageNumberPrevious)}>Previous</button>
		</li>
		{#each numbersPagination as num}
			<li class="page-item">
				<button class="btn-link page-link" on:click={goToPage(num)} class:active={num == pageNumber}
					>{num}</button
				>
			</li>
		{/each}
		<li class="page-item">
			<button class="btn-link page-link" on:click={goToPage(pageNumberNext)}>Next</button>
		</li>
	</ul>
</nav>
