<template>
    <div class="page-order">
        <div class="columns is-multiline">
            <h1 class="title card-header-title">订单</h1>
        </div>

        <div class="column is-12 box">
            <div class="is-fullwidth">
                <OrderItem v-for="order in orders" v-bind:key="order.id" v-bind:initialOrder="order" />
            </div>
        </div>

    </div>
</template>

<style lang="scss">

</style>

<script>
import axios from 'axios'
import OrderItem from '@/components/OrderItem.vue'

export default {
    name: 'orderPage',
    components: {
        OrderItem,
    },
    data() {
        return {
            orders: []
        }
    },
    mounted() {
        this.getOrders()
    },
    methods: {
        async getOrders() {
            await axios
                .get('/api/order/listByUser', {
                    params: {
                        userId: this.$store.getters.getUserInfo.state.user.userId
                    }
                })
                .then(respone => {
                    this.orders = respone.data
                })
                .catch(err => {
                    console.log(err.message);
                })
        }
    }
}
</script>