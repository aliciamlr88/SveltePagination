# sveltebspagination

A simple pagination component for SvelteKit projects.

### Examples

#### Black Color Pagination

![alt text](https://github.com/aliciamlr88/SveltePagination/blob/main/static/pagination-black.jpeg?raw=true)

#### Orange Color Pagination

![alt text](https://github.com/aliciamlr88/SveltePagination/blob/main/static/pagination-orange.jpeg?raw=true)

#### Purple Color Pagination

![alt text](https://github.com/aliciamlr88/SveltePagination/blob/main/static/pagination-purple.jpeg?raw=true)

#### Red Color Pagination

![alt text](https://github.com/aliciamlr88/SveltePagination/blob/main/static/pagination-red.jpeg?raw=true)

## Installation

```
npm i sveltebspagination
```

## Usage

In +page.svelte add the following code wherever you want to put the paginator

```
<script>
    import { Pagination } from 'sveltebspagination';
    export let data;
    $: ({ totalPages } = data);
</script>

<div class="row justify-content-center">
	<div class="col-sm-12 col-md-4">
		<Pagination {totalPages} />
	</div>
</div>
```

In +page.js or +page.server.js add the following code replace `{your_total_pages}` with an integer for the total amount of pages you want to paginate.

```
import { error } from '@sveltejs/kit';
export async function load({ fetch, params, url }) {

    let page = url.searchParams.get('page');

    if(!page){
        page = 1;
    }

    if (isNaN(page) || page <= 0) {
        throw error(400, {
            message: "Page Number must be a number bigger than 0"
        })
    }

    return
       { totalPages: {your_total_pages} };
}
```

## Styles

Customize colors with these classes in global style or +page.svelte style.

```
<style>
    .page-link {
        color: #ff3e00;
    }

    .page-link.active {
        background-color: #ff3e00;
        border-color: #ff3e00;
    }
</style>
```

## Authors

- [Alicia Medina La Rosa](https://github.com/aliciamlr88)
- [Tony Lee](https://github.com/t2ny)
