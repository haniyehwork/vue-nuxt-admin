<template>
    <header class="navbar navbar-dark sticky-top bg-dark flex-md-nowrap p-0 shadow">
        <a class="navbar-brand col-md-3 col-lg-2 me-0 px-3 fs-6" href="#">Company name</a>
        
        <ul class="navbar-nav">
            <li class="nav-item text-nowrap">
                <a class="nav-link px-3" href="javascript:void(0)" @click="logout" >Sign out</a>
            </li>
        </ul>
    </header>
</template>

<script>

import { useRouter } from 'vue-router';

export default{
    name: 'Nav',
    setup() {
        const router = useRouter();

        const logout = () => {
            localStorage.clear();
            router.push('/login');
        }

        return {
            logout
        }
    }
}
</script>
