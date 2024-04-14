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
        // console.log('data', data);
        // console.log('error', error);

        console.log('you are logged in!')
        navigateTo('/confirm')


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
    <h1>Hello there, please login</h1>
    <section>
        <form>
            <label for="email">Type your email</label>
            <input type="email" v-model="email" id="email">
            <label for="pwd">Add a password</label><input type="password" name="password" id="pwd" v-model="password">
            <div class="btn-container"> <button @click.prevent="signUp">Sign In with Email</button>
                <button @click.prevent="logIn">Login</button>
            </div>

            <div class="msgs">
                <p v-if="successMsg">{{ successMsg }}</p>
                <p v-else style="color: red">{{ errorrMsg }}</p>
            </div>
        </form>
    </section>
</template>
<style scoped>
Section {
    display: flex;
    justify-content: center;
}

form {
    display: flex;
    flex-flow: column wrap;
    width: 30em;
    justify-content: center;
    outline: 2px solid #333;
    padding: 1.5rem 1.25rem;
    border-radius: 5px;

    .btn-container {
        display: flex;
        flex-flow: column wrap;
        row-gap: 0.5rem;
        margin-block-start: 0.25rem;

        button {
            margin-inline: auto;
        }
    }
}
</style>
