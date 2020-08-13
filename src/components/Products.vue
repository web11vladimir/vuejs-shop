<template>
    <div class="container">
        <div class="row">
            <div
                class="col-lg-2 col-md-3 col-sm-4 col-6"
                v-for="product in products"
                v-bind:key="product.id"
            >
                <div class="card product-item">
                    <img v-bind:src="product.image" v-bind:class="['card-img']" />
                    <div class="card-body text-center">
                                                
                        <div class="card-title">
                            {{ product.name }}
                        </div>
                        <div class="card-text font-weight-bold">
                            {{ getPrice(product.price) }}
                        </div>
                        <div class="product-addtocart">
                            <button class="btn btn-outline-success"
                                v-on:click="addtocart(product)"
                            >
                                Купить
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Products",
    data: function() {
        return {
            products: null,
        }
    },
    methods: {
        addtocart: function(product) {
            
            let productInCart = false
            // если товар уже в корзине, то увеличиваем количество
            Array.prototype.forEach.call(this.$root.$cart, (item) => {
                 if (item.id == product.id) {
                    item.count++
                    productInCart = true
                }
            })
            
            // если нет в корзине, то добавляем
            if (!productInCart) {
                this.$root.$cart.push({
                    id: product.id,
                    count: 1
                });
            }
        },
        getPrice: function(price) {
            return price + ' ₽'
        }
    },
    mounted() {
        fetch("/products.json")
            .then((response) => response.json())
            .then(data => {
                this.products = data
            })
    }
};
</script>

<style scoped>
    .product-item {
        margin-bottom: 20px;
    }
    .card-img {
        padding: 15px;
    }
    .product-addtocart {
        margin-top: 10px;
    }
</style>