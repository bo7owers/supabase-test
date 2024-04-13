<script setup lang="ts">
const user = useSupabaseUser()

watch(user, () => {
    if (user.value) {
        // redirect to protected page
        return navigateTo('/')
    }
}, { immediate: true })
</script>

<template>
    <p>Waiting for login ...</p>
</template>