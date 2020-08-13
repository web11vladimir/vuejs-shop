<template>
  <div class="cart d-flex flex-column h-100">
        <Header />
        <Cart />
        <Footer/>
    </div>
</template>

<script>
    import Header from '@/components/Header.vue'
    import Cart from '@/components/Cart.vue'
    import Footer from '@/components/Footer.vue'

    export default {
    	name: 'CartPage',
    	components: {
            Header,
            Cart,
    		Footer
    	}
    }
</script>
