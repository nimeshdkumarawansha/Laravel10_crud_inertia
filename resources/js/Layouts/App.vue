<template>
    <div>

        <slot name="content" />
        <slot name="modals" />
    </div>
</template>

<script>
import NavBar from '@/Components/Main/NavBar.vue'

export default {
    components: {
        NavBar
    }
}
</script>

<style lang="css" scoped></style>
