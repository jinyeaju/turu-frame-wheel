<template>
    <div class="seventhContentPage">
        <p>Page-7</p>

        <div class="container" ref="scrollArea">
            <div class="inner"></div>
        </div>
    </div>
</template>
<script>
import { ref, onMounted } from 'vue';
export default {
    name: 'PageSeven',
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
    methods: {
    },
    mounted() {
    },
    setup() {
        const scrollArea = ref(null)

        onMounted(() => {
            scrollArea.value.addEventListener('scroll', onScroll)
        })

        const onScroll = () => {
            console.log('scrollArea.value : '+ scrollArea.value)
        }
        return {
            scrollArea
        }
    },
};
</script>

<style lang="scss" scoped>
// @import "../assets/scss/PageOne.scss";
.seventhContentPage::v-deep {

    .container {
        height: 50vh;
        width: 80%;
        background: yellow;
        overflow-y: scroll;
        margin: 25vh auto;
        .inner {
            height: 200vh;
            width: 90%;
            background: red;
        }
    }
}

</style>