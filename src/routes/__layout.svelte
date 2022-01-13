<script>
	import '../app.scss';
	import Nav from '$lib/components/nav.svelte';

	export let segment
</script>

<Nav {segment}/>

<slot />
