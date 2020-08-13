<template>
    <button v-bind:class="['btn', 'btn-outline-success']" v-on:click="showCart">
        В корзине: {{ cartItemCount }}
    </button>            
</template>

<script>
export default {
    name: "CartMini",
    data: function() {
        return {
            cart: this.$root.$cart,
        };
    },
    computed: {
        cartItemCount: function() {
            let count = 0;
            Array.prototype.forEach.call(this.cart, (item) => {
                count += item.count;
            });
            return count;
        },
    },
    methods: {
        showCart: function() {
            this.$router.push({
                name: "CartPage",
            });
        },
    },
};
</script>
