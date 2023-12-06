<template>
    <main class="container mt-5">
        <div class="row">
            <div class="col-12 text-right mb-4">
                <div class="d-flex justify-content-between">
                    <h3>La Recipes</h3>

                    <nuxt-link to="/recipes/add" class="btn btn-info">Add Recipe</nuxt-link>

                </div>
            </div>
            <template v-if="recipes" v-for="recipe in recipes">
                <div class="col-lg-3 col-md-4 col-sm-6 mb-4">
                    <recipe-card :id="recipe.id" :recipe="recipe"></recipe-card>
                </div>
            </template>
        </div>
    </main>
</template>

<script setup>
import {ref, onMounted} from 'vue'

const recipes = ref([])

// const deleteRecipe = async (id) => {
//     const config = {
//         headers: { "content-type": "multipart/form-data" },
//         method: 'delete'
//     };
//     let response = await fetch(`http://localhost:8000/api/recipes/${id}`, config)
//     recipes.value = await getRecipes()
// }

const getRecipes = async () => {
    const config = {
        headers: { "content-type": "multipart/form-data" }
    };
    let response = await fetch('http://localhost:8000/api/recipes/', config)
    let data = await response.json()

    console.dir(data)

    return data
}

onMounted(async () => {
    recipes.value = await getRecipes()
})
</script>
<style scoped>

</style>