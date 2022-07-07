<template>
    <!-- v-bind로 props할때 :작명="데이터명" 으로 보내주면됨 자식 컴포넌트에서는 작명한걸로 쓰면됨 
    근데 거의 똑같이 쓴다함 부모랑 
    지금 showModal을 modal로 자식한테 보내서 사용중임-->
    <transition name="fade">
        <title-modal
            :onerooms="onerooms"
            :getOneroom="getOneroom"
            :showModal="showModal"
            @closeModal="showModal = false"
        ></title-modal>
    </transition>

    <div class="menu">
        <a v-for="(menu, i) in menus" :key="i">{{ menu }}</a>
    </div>
    <!-- LifeCycle 단계
    create 단계 -> mount 단계 -> 컴포넌트 생성 -> update 단계 unmount 단계
    -->

    <button @click="titleByname">이름순</button>
    <button @click="priceAscending">싼거먼저</button>
    <button @click="priceDescending">비싼거먼저</button>
    <button @click="sortBack">되돌리기</button>

    <dis-count></dis-count>

    <!-- oneroom을 보내도 작동은되는데 굳이 다보낼 필요는 없는거같다 -->
    <!-- $emit으로 받은 놈은 v-on:받은이름 으로 처리하고 받은 데이터는 $event로 처리함 -->
    <card-list
        @openModal="
            showModal = true;
            getOneroom = $event;
        "
        :oneroom="onerooms[i]"
        v-for="(oneroom, i) in onerooms"
        :key="i"
    ></card-list>
</template>


<script>
// 하나의 파일에서 여러가지의 변수를 가져올땐
// import {a,b(가져올변수들)} from '경로' 를 적어주면 됨

// 한가지만 import 할땐
// import 작명 from '경로' 를 적어주면됨
import oneroomData from "./assets/oneroom.js";

// 축약해둔 컴포넌트 쓰는법
// 1. vue 파일 import 해오기
// 2. components에 등록하기
// 3. template안에 태그로 쓰면됨
import DisCount from "./Discount.vue";
import TitleModal from "./TitleModal.vue";
import CardList from "./CardList.vue";

export default {
    name: "App",
    components: {
        // Discount : Discount, 둘이 같으면 축약가능함
        DisCount,
        TitleModal,
        CardList,
    },
    // 동적인 UI를 만들때
    // STEP1. data 에 상태를 저장해둬야함 state라고 한다
    // Step2. data가 변하면 HTML에 넣어야함
    data() {
        return {
            /* [...] 문법은 전개 문법임 사본을 따올때 쓴다.*/
            oneroomsOrigin: [...oneroomData],
            getOneroom: 0,
            onerooms: oneroomData,
            showModal: false,
            menus: ["Home", "Shop", "About"],
            products: ["역삼동원룸", "천호동원룸", "마포구원룸"],
            report: [0, 0, 0],
            showDiscount: true,
        };
    },
    methods: {
        increase() {
            this.report += 1;
        },
        priceAscending() {
            this.onerooms.sort(function (a, b) {
                return a.price - b.price;
            });
        },
        priceDescending() {
            this.onerooms.sort(function (a, b) {
                return b.price - a.price;
            });
        },
        titleByname() {
            this.onerooms.sort(function (a, b) {
                return a.title.localeCompare(b.title);
            });
        },
        sortBack() {
            this.onerooms = [...this.oneroomsOrigin];
        },
    },
    mounted() {},
};
</script>

<style>
body {
    margin: 0;
}

div {
    box-sizing: border-box;
}

.black-bg {
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
    position: fixed;
    padding: 20px;
}

.white-bg {
    width: 100%;
    background: #fff;
    border-radius: 8px;
    padding: 20px;
}

#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
}

.menu {
    background: #42b883;
    padding: 15px;
    border-radius: 5px;
}

.menu a {
    color: #fff;
    padding: 10px;
}

.room-img {
    width: 100%;
    margin-top: 40px;
}

.fade-enter-from {
    /* 시작 */
    transform: translateY(-1000px);
}

.fade-enter-active {
    transition: all 1s;
}

.fade-enter-to {
    /* 끝 */
    transform: translateY(0px);
}

.fade-leave-from {
    /* 시작 */
    opacity: 1;
}

.fade-leave-active {
    transition: all 1s;
}

.fade-leave-to {
    /* 끝 */
    opacity: 0;
}
</style>