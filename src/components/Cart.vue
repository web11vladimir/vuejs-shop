<template>
    <div v-if="checkProductInCart" class="cart-product container">
        <h2 class="text-center mb-4">Корзина</h2>
        <hr />
        <div
            v-for="item in cart"
            v-bind:key="item.id"
            class="product-item row align-items-center"
        >
            <div class="image col-sm-2 col-2">
                <img v-bind:src="getProductImagePath(item)" />
            </div>
            <div class="title col-sm-4 col-5">
                {{ getProductTitle(item) }}
            </div>
            <div class="price col-sm-3 d-none d-sm-block">
                {{ getProductPrice(item) }} x {{ item.count }}
            </div>
            <div class="total-price-item col-sm-2 col-3">
                <strong>{{ getProductTotalPrice(item) }}</strong>
            </div>
            <div class="col-sm-1 col-1">
                <button
                    v-bind:class="'delete-btn'"
                    v-on:click="deleteProduct(item)"
                >
                    <img src="@/assets/trash.svg" alt="" />
                </button>
            </div>
            <div class="col-12">
                <hr />
            </div>
        </div>
        <div class="total-price text-right">
            Итого: <strong>{{ getTotalPriceCart() }}</strong>
        </div>

        <UserForm v-on:clearCart="deleteAllproduct" />
    </div>
    <div v-else class="cart-product container">
        <div class="alert alert-info">Корзина пуста</div>
    </div>
</template>

<script>
import UserForm from "@/components/UserForm.vue";

export default {
    name: "Cart",
    components: {
        UserForm,
    },
    data: function() {
        return {
            cart: this.$root.$cart,
            products: false,
            fetching: false,
        };
    },
    computed: {
        // проверка на наличие товаров в корзине
        checkProductInCart: function() {
            return this.cart.length;
        },
    },
    methods: {
        // получаем путь к картинке
        getProductImagePath: function(item) {
            let id = item.id;

            for (let i = 0; i < this.products.length; i++) {
                if (this.products[i].id == id) {
                    return this.products[i].image;
                }
            }
        },
        // получаем название товара
        getProductTitle: function(item) {
            let id = item.id;

            for (let i = 0; i < this.products.length; i++) {
                if (this.products[i].id == id) {
                    return this.products[i].name;
                }
            }
        },
        // получаем цену товара
        getProductPrice: function(item) {
            let id = item.id;

            for (let i = 0; i < this.products.length; i++) {
                if (this.products[i].id == id) {
                    return this.products[i].price + " ₽";
                }
            }
        },
        // получаем цену с у четом количества
        getProductTotalPrice: function(item) {
            let id = item.id;

            for (let i = 0; i < this.products.length; i++) {
                if (this.products[i].id == id) {
                    return this.products[i].price * item.count + " ₽";
                }
            }
        },
        // получаем общую цену корзины
        getTotalPriceCart: function() {
            let result = 0;

            for (let i = 0; i < this.cart.length; i++) {
                for (let j = 0; j < this.products.length; j++) {
                    if (this.products[j].id == this.cart[i].id) {
                        result += this.products[j].price * this.cart[i].count;
                    }
                }
            }

            return result + " ₽";
        },
        // удаляем товар
        deleteProduct: function(item) {
            for (let i = 0; i < this.cart.length; i++) {
                if (this.cart[i].id == item.id) {
                    this.cart.splice(i, 1);
                }
            }
        },
        // очищаем корзину
        deleteAllproduct: function() {
            this.cart.splice(0, this.cart.length);
        },
    },
    mounted() {
        fetch("/products.json")
            .then((response) => response.json())
            .then((data) => {
                this.products = data;
                this.fetching = true;
            });
    },
};
</script>

<style scoped>
.image {
    text-align: center;
}
.image img {
    max-height: 50px;
}
.delete-btn {
    background: none;
    border: none;
    outline: none;
    padding: 0;
}
.delete-btn img {
    height: 18px;
}
</style>
