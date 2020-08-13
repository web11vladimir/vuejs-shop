<template>
    <div class="home d-flex flex-column h-100">
        <Header />
        <Products />
        <Footer />
    </div>
</template>

<script>
    import Header from '@/components/Header.vue'
    import Products from '@/components/Products.vue'
    import Footer from '@/components/Footer.vue'

    export default {
        name: 'Home',
        components: {
            Header, 
            Products,
            Footer
        }
    }
</script>