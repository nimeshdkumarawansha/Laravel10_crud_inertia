<template>
    <div>
        <nav class="navbar navbar-default">
            <div class="container-fluid">
                <ul class="nav navbar-nav">
                    <li class="active"><Link :href="route('dashboard')">Home</Link></li>
                    <!-- <li><Link :href="route('todo')">Page 1</Link></li> -->
                    <li><a href="#">Page 2</a></li>
                    <li><a href="#">Page 3</a></li>
                </ul>
                <Link :href="route('login')">Login</Link> ||
                <Link :href="route('register')">Register</Link>
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
