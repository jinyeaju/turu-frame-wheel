<template>
    <header>
        <!-- <div class="logoArea">
            <img src="" alt="">
        </div> -->
        <ul>
            <li class="active"><a href="#">Page1</a></li>
            <li><a href="#">Page2</a></li>
            <li><a href="#">Page3</a></li>
            <li><a href="#">Page4</a></li>
            <li><a href="#">Page5</a></li>
            <li><a href="#">Page6</a></li>
            <li><a href="#">Page7</a></li>
        </ul>
    </header>
</template>
<script>
export default {
    name: 'HeaderArea',
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
    setup() {
        

        return {
        }
    },
};
</script>

<style lang="scss">
// @import "../assets/scss/header-area.scss";
</style>