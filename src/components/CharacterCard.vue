<template>
<div class="card">
    <header class="card-header">
        <p class="card-header-title">
        {{character.name}}
        </p>
    </header>
    <div class="card-image">
        <figure class="image is-4by3">
            <img :src="character.image" alt="Placeholder image">
        </figure>
    </div>
    <div class="card-content">
        <div class="content">
            
        </div>
    </div>
</div>
</template>

<script>
export default {
    props: ['character']
}
</script>

<style>
</style>