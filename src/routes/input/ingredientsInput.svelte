<script>
    import supabase from "$lib/db";
    import __layout from "../__layout.svelte";

    // add new ingredient
    let newIngredient;
    let submit = false;

    async function sendData() {
        const { data, error } = await supabase
            .from('ingredient')
            .insert([
                { 'name': newIngredient }
            ])

        if (error) throw new Error(error.message) 
        return data
    }

    // view ingredient
    async function getData() {
    const { data, error } = await supabase
        .from('ingredient')
        .select()
    if (error) throw new Error(error.message)
    
    return data
    }

    function handelSubmit(event) {
        const formData = new FormData(event.target);
        // const formDataObject = Object.fromEntries(formData);
        // console.log(formData);
        console.log(Object.fromEntries(formData.value));
        // event.target.reset();
        
    }
</script>

<form on:submit|preventDefault={handelSubmit}>
    <input type="text" name="Zutat" bind:value={newIngredient}>
    <button type="submit">Eintragen</button>
</form>

{#if submit}
    {#await sendData()}
        <p>Zutat wird gespeichert ...</p>
    {:then data} 
        <p>Zutat wurde gespeichert</p>
     {:catch error}
        <p>Etwas ist schief gegangen</p>
        <pre>{ error }</pre>   
    {/await}
{/if}

<h1>Zutaten liste</h1>
{#await getData()}
  <p>Fetching data...</p>
{:then data}
  {#each data as ingredient}
    <li>{ingredient.name}</li>
  {/each}
{:catch error}
  <p>Something went wrong while fetching the data:</p>
  <pre>{error}</pre>
{/await}