<script>
    import supabase from "$lib/db";
    import Layout from "./__layout.svelte";
    
    async function getData() {
        const { data , error } = await supabase
            .from('recipe')
            .select()
        
        if (error) throw new Error (error.message)

        return data
    }
</script>

<h1>Rezepte</h1>

{#await getData()}
    <p>Rezepte werden geladen...</p>
{:then data} 
    {#each data as recipe }
        <li>{recipe.name}</li>
    {/each}
{:catch error}
    <p>Da ist etwas schief gegangen</p>
    <pre>{error}</pre>
{/await}
