<script>
    import supabase from "$lib/db";
    import __layout from "../__layout.svelte";

    // add new recipe
    let newRecipeName;
    let newRecipeKitchen;
    let newRecipeBook;
    let newRecipePage;
    let newRecipeIngredient;
    let newIngredientAmount;
    let newIngredientUnit;

    let dataPromise;

    dataPromise = getData();

    async function getData() {
        const { data, error } = await supabase
            .from('recipe')
            .select()
        const {data: ingredientInRecipe, error: ingredientInRecipe} = await supabase
            .from('ingredientInRecipe')
            .select()
        if (error) throw new Error(error.message)

        return data
    }

</script>

{#await dataPromise}
    <p>Daten werden geladen...</p>
{:then data}
    {#each data as recipe}
        <div>
            <h3>{recipe.name}</h3>
            <p>
                {recipe.kitchen}
            </p>
            <p>
                {recipe.book}
            </p>
            <p>
                {recipe.page}
            </p>
            <p>
                {#each data: in as }
                    
                {/each}
            </p>
        </div>
    {/each}
    
{/await}