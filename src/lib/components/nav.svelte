<script>

    import { page } from "$app/stores";

    $:segment = $page.url.pathname;

</script>

<nav>
    <a aria-current={'/' === $page.url.pathname ? 'page' : undefined} href="/">Home</a>
    <a aria-current={'/' === $page.url.pathname ? 'page' : undefined} href="/input/ingredientsInput">Zutaten eingabe</a>
</nav>