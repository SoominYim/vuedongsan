<template>
    <div>
        <img :src="oneroom.image" alt="" class="room-img" />
        <!-- $emit => 부모에게 보내자 ('작명',데이터) -->
        <h4 @click="sendModal">{{ oneroom.title }}</h4>
        <p>{{ oneroom.price }}원</p>
    </div>
</template>

<script>
export default {
    name: "CardList",
    props: {
        oneroom: Object,
    },
    methods: {
        sendModal() {
            // ('전달할이름',전달할데이터)
            this.$emit("openModal", this.oneroom.id);
        },
    },
};
</script>

<style>
</style>