<template>
    <div class="eighthContentPage" >
        <!--  -->
        <div class="innerTabBox" ref="scrollArea">
            <div class="contBox one"></div>
            <div class="contBox two"></div>
            <div class="contBox three"></div>
            <div class="contBox four"></div>
            <div class="contBox five"></div>
            <div class="contBox six"></div>
        </div>
    </div>
</template>
<script>
import { ref, onMounted, onBeforeUnmount } from 'vue';
export default {
    name: 'PageEight',
    components: {
    },
    props: {
        // hPercent : Number
    },
    data() {
		return {
            // heightPercentage: this.hPercent,

        }
	},
    setup() {
        const heightPercentage = ref(null)
        const scrollArea = ref(null)

        onMounted(() => {
            scrollArea.value.scrollTo(0, 0);
            scrollArea.value.addEventListener('wheel', onMouseScroll);
        })
        onBeforeUnmount(() => {
            scrollArea.value.removeEventListener('wheel', onMouseScroll);
        })
        const onMouseScroll = ((event) => {
            console.log("scrolling,,,")
            // vh 구하기
            heightPercentage.value = scrollArea.value.offsetHeight / scrollArea.value.clientHeight * 100
            console.log("scrollArea.value.scrollY : "  + scrollArea.value.scrollY);
            console.log("scrollArea.value.scrollTop : "  + heightPercentage.value);
            console.log(event)
            console.log(scrollArea.value)
            console.log(event.deltaY)

        })



        return {
            // heightPercentage,
            scrollArea,
        }
    },
};
</script>

<style lang="scss" scoped>
// @import "../assets/scss/PageOne.scss";
.eighthContentPage::v-deep {
    width: 80%;
    height: 80vh;
    background: white;
    margin: 10vh auto;
    overflow:auto;
    .innerTabBox {
        display: flex;
        flex-wrap: wrap;
        .contBox {
            width: calc(100% / 3 - 20px); height: 400px;
            background-color: #ffa;
            margin: 0 10px 20px;
        }
    }
}

</style>