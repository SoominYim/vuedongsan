<template>
    <div class="black-bg" v-if="showModal">
        <!-- v-if는 참일때 ui가 보이게함 -->
        <div class="white-bg">
            <!-- v-for문 아닌 곳에서 사용하려면 index에 변수를 넣어줘야한다.
        그 변수는 v-for문에서 가져오면된다. -->
            <img :src="onerooms[getOneroom].image" alt="" class="room-img" />
            <h4>{{ onerooms[getOneroom].title }}</h4>
            <p>{{ onerooms[getOneroom].content }}</p>
            <input type="number" v-model.number="month" />

            <p>
                {{ month }}개월 선택함
                {{ onerooms[getOneroom].price * month }}원
            </p>
            <button @click="$emit('closeModal')">닫기</button>
        </div>
    </div>
</template>

<script>
export default {
    name: "TitleModal",
    data() {
        return {
            month: "",
        };
    },
    // month라는 v-model을 감시함
    watch: {
        // 파라미터 a는 input 입력된값임 (a,b) b는 변경전 데이터임
        month(a) {
            if (isNaN(a) == true || a.trim) {
                alert("문자 입력하지마셈");
                this.month = 1;
            }
        },
    },
    beforeUpdate() {
        if (this.month == 2) {
            alert("넘작앙");
            this.month = 3;
        }
    },
    props: {
        // 틀려도 에러는 나지않음 , 잘못 타입이 전달되는경우 브라우저 스크립트콘솔에 경고나옴
        onerooms: Array,
        getOneroom: Number,
        showModal: Boolean,
    },
    methods: {},
};
</script>

<style>
</style>