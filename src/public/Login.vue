<template>
    <form class="form-signin" @submit.prevent="submit">
        <h1 class="h3 mb-3 fw-normal">Please login</h1>

        <input type="email" class="form-control" id="floatingInput" placeholder="name@example.com" required v-model="email">
        <label for="floatingInput">Email address</label>

        <input type="password" class="form-control" id="floatingPassword" placeholder="Password" required v-model="password">
        <label for="floatingPassword">Password</label>

        <button class="w-100 btn btn-lg btn-primary" type="submit">Login</button>
    </form>
</template>

<script>
import {ref} from 'vue';
import axios from 'axios';
import { useRouter } from 'vue-router';

export default {
    name: 'Login',
    setup() {
        const email = ref('');
        const password = ref('');
        const router = useRouter();

        const submit = async () => {
            const response = await axios.post('login', {
                email: email.value,
                password: password.value
            });

            localStorage.setItem('token', response.data.token);
            axios.defaults.headers.common["Authorization"] = `Bearer ${response.data.token}`;

            await router.push('/');
            console.log(axios.defaults);

        };

        return {
            email,
            password,
            submit
        }
    }
}
</script>


<style scoped>
    html,
    body {
        height: 100%;
    }

    body {
        display: flex;
        align-items: center;
        padding-top: 40px;
        padding-bottom: 40px;
        background-color: #f5f5f5;
    }

    .form-signin {
        max-width: 330px;
        padding: 15px;
    }

    .form-signin .form-floating:focus-within {
        z-index: 2;
    }

    .form-signin input[type="email"] {
        margin-bottom: -1px;
        border-bottom-right-radius: 0;
        border-bottom-left-radius: 0;
    }

    .form-signin input[type="password"] {
        margin-bottom: 10px;
        border-top-left-radius: 0;
        border-top-right-radius: 0;
    }
</style>