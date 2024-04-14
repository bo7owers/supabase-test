<script setup lang="ts">
const user = useSupabaseUser()

</script>

<template>
    <p>Hi {{ user?.email }}</p>
</template>