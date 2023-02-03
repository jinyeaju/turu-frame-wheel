<template>
    <HeaderArea class="header"/>
    <div class="page" ref="mainPage">
      <!--  @wheel="onUseWheel" -->
      <div class="box"><PageOne/></div>
      
      <div class="box"><PageTwo/></div>
      
      <div class="box"><PageThree/></div>
      
      <div class="box"><PageFour/></div>
      
      <div class="box"><PageFive/></div>
     
      <div class="box"><PageSix/></div>
      
      <div class="box"><PageSeven/></div>

      <!-- <div class="relativeBox" ref="relativeBox"><PageEight/></div> -->
      
    </div>

    <!-- <main>
        <section class="box active"><p>Page-1</p></section>
    </main> -->
</template>

<script>
import { ref, onMounted, onBeforeUnmount } from 'vue'
// import { onMounted, ref } from 'vue'
import HeaderArea from './components/HeaderArea.vue'
import PageOne from './components/PageOne.vue'
import PageTwo from './components/PageTwo.vue'
import PageThree from './components/PageThree.vue'
import PageFour from './components/PageFour.vue'
import PageFive from './components/PageFive.vue'
import PageSix from './components/PageSix.vue'
import PageSeven from './components/PageSeven.vue'
// import PageEight from './components/PageEight.vue'

export default {
  name: 'App',
  components: {
    HeaderArea,
    PageOne,
    PageTwo,
    PageThree,
    PageFour,
    PageFive,
    PageSix,
    PageSeven,
    // PageEight,
  },
  data() {
    return {

    }
  },
  methods: {
  },
  setup() {
    // const heightPercentage = ref(null)
    const mainPage = ref(null)
    const relativeBox = ref(null)
    const setList = ref(
      {
        activePageIndex : 1,
        eventRoading: false,
        emptyArr: [],
      }
    )

    onMounted(() => {
      window.scrollTo(0, 0);
      
      window.addEventListener("wheel", function(e){
        e.preventDefault();
      },{passive : false});

      document.addEventListener('wheel', onMouseWheel);
      setList.value.activePageIndex = 1;

      const boxArray = mainPage.value.children;
      for(let i = 0; i < boxArray.length; i++){
        // console.log(boxArray[i].getBoundingClientRect().top);
        setList.value.emptyArr[i] = `${boxArray[i].getBoundingClientRect().top}`;
      }
      console.log(setList.value.emptyArr);

      // // add scroll
      // document.addEventListener('scroll', onMouseScroll);

    })
    onBeforeUnmount(() => {
      document.removeEventListener('wheel', onMouseWheel);
    })
    
    
    
    const onMouseWheel = ((event) => {
      if(setList.value.eventRoading === true){
        // document.removeEventListener('wheel', onMouseWheel);
        // event.stopImmediatePropagation();
        return;
      }
      // event.stopImmediatePropagation();

      // event chceck
      // console.log(event)

      // console.log(setList.value.activePageIndex + 1)

      setList.value.eventRoading = true;
      setTimeout(() => {
        setList.value.eventRoading = false;
        // console.log("setList.value.eventRoading : "+setList.value.eventRoading)
      }, 400);
      // console.log("setList.value.eventRoading : "+setList.value.eventRoading)

      if(setList.value.activePageIndex < 1){
        setList.value.activePageIndex = 1;
        mainPage.value.style.transform = "translateY(0)"
      }else{
        if(setList.value.activePageIndex >= 7){
          setList.value.activePageIndex = 7;
          mainPage.value.style.transform = "translateY(-600vh)"
          // document.removeEventListener('wheel', onMouseWheel);
          console.log("removeEventListener")
          // add scroll
          // document.addEventListener('scroll', onMouseScroll);
          console.log("addEventListener")
        }else{
          console.log("event.deltaY : "+event.deltaY )
          if(event.deltaY < 0){
            console.log("setList.value.activePageIndex : "+setList.value.activePageIndex )
            setList.value.activePageIndex = Math.max(1, setList.value.activePageIndex - 1);
            // setList.value.activePageIndex--;
            mainPage.value.style.transform = "translateY("+Math.min(0, (-100 * (setList.value.activePageIndex - 1)))+"vh)"
            // mainPage.value.style.transform = "translateY(-"+100 * (setList.value.activePageIndex - 1)+"vh)"
            // mainPage.value.style.transform = "translateY(-"+setList.value.emptyArr[setList.value.activePageIndex - 1]+"px)"
            mainPage.value.style.transition = "all 0.3s ease-out"
            // window.scrollTo(0, setList.value.emptyArr[setList.value.activePageIndex - 1])
            console.log(mainPage.value)
          }else{
            console.log("setList.value.activePageIndex : "+setList.value.activePageIndex)
            // setList.value.activePageIndex = Math.min(8, setList.value.activePageIndex + 1);
            setList.value.activePageIndex++;
            mainPage.value.style.transform = "translateY("+Math.max(-600, (-100 * (setList.value.activePageIndex - 1)))+"vh)"
            // mainPage.value.style.transform = "translateY(-"+100 * (setList.value.activePageIndex - 1)+"vh)"
            // mainPage.value.style.transform = "translateY(-"+setList.value.emptyArr[setList.value.activePageIndex - 1]+"px)"
            mainPage.value.style.transition = "all 0.3s ease-out"
            // window.scrollTo(0, setList.value.emptyArr[setList.value.activePageIndex - 1])
            console.log(mainPage.value)
          }
        }
      }
      // mainPage.value.style.overflow = "hidden !important";
    });

    // const onMouseScroll = ((event) => {
    //   // vh 구하기
    //   heightPercentage.value = window.scrollY / window.outerHeight * 100
    //   console.log("window.scrollTop : "  + heightPercentage.value);
    //   console.log(event)
    // })
    // async function eventCaller(){
    //   console.log("Caller");
    //   await onMouseWheel;
    //   console.log("After waiting");
    // }

    // eventCaller();

    // const onUseWheel = ((e) => {
    //   console.log("마우스 휠 이벤트 작동")
    //   // e.preventDefault()
    //   // console.log(e)
    //   // console.log(e.wheelDelta)
    //   console.log("e.wheelDelta :"+e.wheelDelta) 
    //   if(e.wheelDelta > 0){ 
    //     if(setList.value.activePageIndex == 0){
    //       return;
    //     }else{
    //       setList.value.activePageIndex--;
    //       console.log(setList.value.activePageIndex)
    //       console.log("window.innerHeight : "+window.innerHeight)
    //       console.log("setList.value.activePageIndex : "+setList.value.activePageIndex)
    //       console.log("window.innerHeight * setList.value.activePageIndex: " + window.innerHeight * setList.value.activePageIndex)
    //       // window.scrollTo(0, (window.innerHeight * setList.value.activePageIndex - 10));
    //       // window.scrollTop = window.innerHeight * setList.value.activePageIndex;
    //       mainPage.value.style.transform = "translateY("+setList.value.activePageIndex * 100+"vh)"
    //     }
    //   }else{
    //     const lastPage = mainPage.value.children.length
    //     // console.log("lastPage : "+ lastPage)
    //     if(setList.value.activePageIndex == lastPage){
    //       return;
    //     }else{
    //       setList.value.activePageIndex++;
    //       console.log("window.innerHeight : "+window.innerHeight)
    //       console.log("setList.value.activePageIndex : "+setList.value.activePageIndex)
    //       console.log(setList.value.activePageIndex)
    //       console.log("window.innerHeight * setList.value.activePageIndex: " + window.innerHeight * setList.value.activePageIndex)
    //       // window.scrollTo(0, (window.innerHeight * setList.value.activePageIndex - 10));
    //       // window.scrollTo({top: window.innerHeight * setList.value.activePageIndex, left:0, behavior: "smooth"});
    //       // window.scrollTop = window.innerHeight * setList.value.activePageIndex;
    //       mainPage.value.style.transform = "translateY("+setList.value.activePageIndex * 100+"%)"
    //     }
    //   }
    // })
      
      // window.addEventListener("wheel", () => {

        // const hEvenet = new WheelEvent(wheel, deltaY);
        // console.log(hEvenet)
        // console.log(mainPage.value)
        // console.log(mainPage.value.children)
        // console.log(mainPage.value.children[0])
        // const boxArray = mainPage.value.children;
      //   boxArray.forEach(function(item, index){
      //     console.log(e)
      //     console.log(item)
      //     console.log(index)
      //   });
        // for(let i = 0; i < boxArray.length; i++){
        //   // console.log(boxArray[i].className);
        //   if(boxArray[i].className == "box active"){
        //     console.log(boxArray[i].className);
        //   }
        // }
      // })


    // });
    return {
      mainPage,
      setList,
      relativeBox,
      // onMouseWheel,
    }
  },
} 
</script>

<style lang="scss">
  @import "./assets/scss/main.scss";
  body {
    margin: 0; padding: 0;
  }
  .header { display: none;}
  .page{ height: 700vh; width: 100%; position: relative; transform: translateY(0);}
  .page .box{
    position: absolute;
    top: 0;
    left: 50%;
    transform: translateX(-50%);
    width: 100%; height: 100vh;
  }
  .page .box:nth-child(1){ background-color: red; z-index: 7; top: 0;}
  .page .box:nth-child(2){ background-color: orange; z-index: 6; top: 100vh;}
  .page .box:nth-child(3){ background-color: yellow; z-index: 5; top: 200vh;}
  .page .box:nth-child(4){ background-color: green; z-index: 4; top: 300vh;}
  .page .box:nth-child(5){ background-color: blue; z-index: 3; top: 400vh;}
  .page .box:nth-child(6){ background-color: purple; z-index: 2; top: 500vh;}
  .page .box:nth-child(7){ background-color: violet; z-index: 1; top: 600vh;}
  .page .box:nth-child(8){}
  .page .box div{
    position: fixed;
    width: 100%; height: 100vh;
    top: 0; 
    left: 50%;
    transform: translateX(-50%);
    font-size: 40px;
    font-weight: bold;
    color: #fff;
    text-shadow: 0 0 4px #222;
  }
  .page .relativeBox{ 
    position: absolute;
    top: 700vh;
    width: 100%;
    height: 100vh;
    background-color: pink; 
    z-index: 1;
  }


</style>
