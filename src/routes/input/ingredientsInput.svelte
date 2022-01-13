<script lang="ts">
    import supabase from "$lib/db";
    import __layout from "../__layout.svelte";

    // add new ingredient
    let newIngredient;
    let dataPromise;

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
    dataPromise = getData();

    async function getData() {
        const { data, error } = await supabase
            .from('ingredient')
            .select()
        if (error) throw new Error(error.message)
        
        return data
    }

    async function handelSubmit(event:FormDataEvent) {
        const form = event.target as HTMLFormElement;
        const formData = new FormData(form);
        // @ts-ignore
        const formDataObject = Object.fromEntries(formData);
        try {
            await sendData()
            dataPromise = getData();
            form.reset();
        }
        catch(error) {
            console.log(error);
        }
    }
</script>

<form on:submit|preventDefault={handelSubmit}>
    <input type="text" name="Zutat" bind:value={newIngredient}>
    <button type="submit">Eintragen</button>
</form>

<h1>Zutaten liste</h1>
{#await dataPromise}
  <p>Fetching data...</p>
{:then data}
  {#each data as ingredient}
    <li>{ingredient.name}</li>
  {/each}
{:catch error}
  <p>Something went wrong while fetching the data:</p>
  <pre>{error}</pre>
{/await}