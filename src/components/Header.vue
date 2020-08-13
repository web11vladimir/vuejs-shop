<template>
    <nav class="navbar navbar-light bg-light">
        <div class="container">
            <router-link to="/" v-bind:class="'navbar-brand'"> VueShop</router-link>
            <CartMini />
        </div>
    </nav>
</template>

<script>
import CartMini from "@/components/CartMini.vue";

export default {
    name: "Header",
    components: {
        CartMini,
    },
};
</script>

<style scoped>
.navbar {
    position: fixed;
    top: 0;
    z-index: 9;
    width: 100%;
}
</style>
