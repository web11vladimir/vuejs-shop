<template>
    <div class="user-form">
        <form action="" v-on:submit.prevent="submitForm">
            <div class="form-group">
                <label for="nameField">Имя</label>
                <input
                    v-model="name"
                    type="text"
                    id="nameField"
                    class="form-control"
                    required="required"
                />
            </div>
            <div class="form-group">
                <label for="namePhone">Телефон</label>
                <input
                    v-model="phone"
                    type="tel"
                    id="namePhone"
                    class="form-control"
                    required="required"
                />
            </div>

            <div class="form-group text-center">
                <button
                    v-on:submit="submitForm"
                    class="btn btn-success"
                    type="submit"
                >
                    Оформить заказ
                </button>
            </div>
        </form>
    </div>
</template>

<script>
export default {
    name: "UserForm",
    data: function() {
        return {
            name: "",
            phone: "",
            cart: this.$root.$cart,
          
        };
    },
    methods: {
        submitForm: function() {
            alert(
                this.name +
                    ", спасибо за заказ!\n" +
                    "На телефон " +
                    this.phone +
                    " было отправлено смс."
            )
            
            this.$emit('clearCart');
        },
    },
};
</script>

<style>
.user-form {
    margin: 30px 0;
}
</style>
