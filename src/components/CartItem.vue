<template>
    <tr>
        <td><input class="check" type="checkbox" @click="checkItem()"></td>
        <td>{{ item.name }}</td>
        <td>${{ item.price }}</td>
        <td>
            <button @click="decrementnum(item)" style="padding: 0 8px">-</button>
            {{ item.num }}
            <button @click="incrementnum(item)" style="padding: 0 8px">+</button>
        </td>
        <td>${{ getItemTotal(item).toFixed(2) }}</td>
        <td><button class="delete" @click="removeCartItem(item)"></button></td>
    </tr>

</template>



<script>
export default {
    name: 'CartItem',
    props: {
        initialItem: Object
    },
    data() {
        return {
            item: this.initialItem
        }
    },
    methods: {
        getItemTotal(item) {
            this.updateCart()
            return item.num * item.price
        },
        incrementnum(item) {
            item.num++
            this.updateCart()
        },
        decrementnum(item) {
            item.num--
            if (item.num == 0) {
                this.$emit('removeCartItem', item)
            }
            this.updateCart()
        },
        updateCart() {
            // localStorage.setItem('cart', JSON.stringify(this.cart))
            this.$emit('updateTotalPrice')
        },
        removeItem(item) {
            this.$emit('removeItem', item)
            this.updateCart()
        },
        removeCartItem(item) {
            this.$emit('removeCartItem', item)
        },
        checkItem() {
            this.item["check"] = !this.item["check"]
            this.$emit('updateTotalPrice')
            this.$emit('conbindCartList')
        }
    },
}
</script>