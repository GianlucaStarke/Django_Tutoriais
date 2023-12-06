<template>
    <div class="card recipe-card">
        <img :src="recipe.picture" class="card-img-top">
        <div class="card-body">
            <h5 class="card-title">{{ recipe.name }}</h5>
            <p class="card-text">
                <strong>Ingredients:</strong> {{ recipe.ingredients }}
            </p>
            <div class="action-buttons">

                <nuxt-link :to="`/recipes/${recipe.id}/`" class="btn btn-sm btn-success">View</nuxt-link>

                <nuxt-link :to="`/recipes/${recipe.id}/edit/`" class="btn btn-sm btn-primary">Edit</nuxt-link>

                <button @click="deleteRecipe(recipe.id)" class="btn btn-sm btn-danger">Delete</button>

            </div>
        </div>
    </div>
</template>

<script setup>
defineProps([
    'recipe',
    'id'
])

const deleteRecipe = async (id) => {
    const config = {
        headers: { "content-type": "multipart/form-data" },
        method: 'delete'
    };
    let response = await fetch(`http://localhost:8000/api/recipes/${id}`, config)
    document.location.reload()
}

// export default {
//     props: ["recipe", "onDelete"]
// };
</script>

<style>
.recipe-card {
    box-shadow: 0 1rem 1.5rem rgba(0, 0, 0, .6);
    min-width: 253px;
}
</style>