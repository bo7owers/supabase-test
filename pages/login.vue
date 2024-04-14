<script setup lang="ts">
const supabase = useSupabaseClient()
const email = ref('')
const password = ref('')
const errorrMsg = ref<unknown>()
const successMsg = ref('')
const isSignedUp = ref(true)

async function signUp() {
    // clear up divs
    errorrMsg && (errorrMsg.value = '')
    successMsg && (successMsg.value = '')
    try {
        const { data, error } = await supabase.auth.signUp({
            email: email.value,
            password: password.value
        })
        console.log('data', data);
        console.log('error', error);

    } catch (error) {
        errorrMsg.value = error
    }
}

async function logIn() {
    try {
        const { data, error } = await supabase.auth.signUp({
            email: email.value,
            password: password.value,
        })
        console.log('data', data);
        console.log('error', error);

        // alert('you are logged in!')
        navigateTo('/')


    } catch (error) {
        errorrMsg.value = error
    }
}

const user = useSupabaseUser()
onMounted(() => {
    watchEffect(() => {
        if (user.value) {
            navigateTo('/')
        }
    })
})

</script>
<template>
    <h1>Login</h1>
    <form>
        <label for="email">Type your email</label>
        <input type="email" v-model="email" id="email">
        <label for="pwd">Add a password</label><input type="password" name="password" id="pwd" v-model="password">
        <button @click.prevent="signUp">Sign In with Email</button>
        <button @click.prevent="logIn">Login</button>

        <div class="msgs">
            <p v-if="successMsg">{{ successMsg }}</p>
            <p v-else style="color: red">{{ errorrMsg }}</p>
        </div>
    </form>
</template>