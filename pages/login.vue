<script setup lang="ts">
const supabase = useSupabaseClient()
const email = ref('')
const password = ref('')
const errorrMsg = ref<unknown>()
const successMsg = ref('')

async function signUp() {
    // clear up divs
    errorrMsg && (errorrMsg.value = '')
    successMsg && (successMsg.value = '')
    try {
        const { data, error } = await supabase.auth.signUp({
            email: email.value,
            password: password.value
        })

        !error && (successMsg.value = 'Check your email to confirm your account.')
        throw error
    } catch (error) {
        errorrMsg.value = error
    }
}
</script>
<template>
    <h1>Login</h1>
    <form>
        <label for="email">Type your email</label>
        <input type="email" v-model="email" id="email">
        <label for="pwd">Add a password</label><input type="password" name="password" id="pwd">
        <button @click.prevent="signUp">Sign In with Email</button>
        <div class="msgs">
            <p v-if="successMsg">{{ successMsg }}</p>
            <p v-else>{{ errorrMsg }}</p>
        </div>
    </form>
</template>