<template>
    <div>
        <nav class="navbar navbar-default mb-5">
            <div class="container-fluid">
                <ul class="nav navbar-nav">
                  
                </ul>
                <Link :href="route('login')" class="link-success fw-bold">Login</Link> ||
                <Link :href="route('register')" class="link-success fw-bold">Register</Link>
            </div>
        </nav>
    </div>
</template>

<script>
import { Link } from '@inertiajs/vue3';
export default{
    components : {
        Link
    }
}
</script>

<style lang="scss" scoped></style>
