<template>
    <div v-if="discount" class="discount">
        <h4>지금 결제하면 {{ discount }}% 할인</h4>
    </div>
</template>

<script>
export default {
    name: "DisCount",
    data() {
        return {
            discount: 30,
        };
    },
    methods: {},
    mounted() {
        let countDown = setInterval(() => {
            this.discount--;
            if (this.discount == 0) {
                clearInterval(countDown);
                this.discount = false;
            }
        }, 1000);
    },
};
</script>

<style>
.discount {
    background: #eee;
    padding: 10px;
    margin: 10px;
    border-radius: 5px;
}
</style>