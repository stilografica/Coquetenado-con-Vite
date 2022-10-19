<script setup>
const information = defineProps({
    title: String,
    id: Number,
    body: {
    type: String,
      default: 'Sin descripción'
    }
})
</script>

<template>
  <div class="card my-2">
    <div class="card-body"> 
        <h5 class="card-title">{{information.title}} #{{information.id}}</h5>
        <p>{{information.body}}</p>
    </div>
    </div>
</template>

<style scoped>
</style>
