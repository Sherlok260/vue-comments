<template>
    <div class="d-flex justify-content-end">
        <button @click="$router.push('/')" class="btn">Home</button>
        <nav class="mt-md-0 ms-md-auto">
            <button @click="$router.push('/comment')" class="btn">Comments</button>
            <button @click="$router.push('/about')" class="btn">About</button>
        </nav>
    </div>
</template>

<script>
export default {

}
</script>

<style>
 
</style>