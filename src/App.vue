<script setup>
  import {ref, reactive, onMounted, onUnmounted} from 'vue'

  const activeIndex = ref(0)

  const carouselItems = [
    {
      image: 'https://images.unsplash.com/photo-1573843981267-be1999ff37cd?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1074&q=80',
      title: 'Sun Siyam Iru Veli',
      caption: 'Nulla vitae elit libero, a pharetra augue mollis interdum. Nulla vitae elit libero, a pharetra augue'
    },
    {
      image: 'https://images.unsplash.com/photo-1573935392379-e9367b718ef1?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1056&q=80',
      title: 'Sun Siyam olhu Veli',
      caption: 'Nulla vitae elit libero, a pharetra augue mollis interdum.'
    },
    {
      image: 'https://images.unsplash.com/photo-1647426130233-66a93ff4a516?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1074&q=80',
      title: 'Siam World',
      caption: 'Nulla vitae elit libero, a pharetra augue mollis interdum.'
    },
    {
      image: 'https://images.unsplash.com/photo-1618238832760-7e4129ef4a43?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80',
      title: 'Water Resort',
      caption: 'Nulla vitae elit libero, a pharetra augue mollis interdum.'
    },
    {
      image: 'https://images.unsplash.com/photo-1602002418655-57aef867418e?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1074&q=80',
      title: 'Sea Beach Resort',
      caption: 'Nulla vitae elit libero, a pharetra augue mollis interdum.'
    }
  ]

  const imageFilter = '-webkit-filter: grayscale(100%);filter: grayscale(100%);'

  const incrementActiveIndex = () =>{
    if(activeIndex.value == carouselItems.length -1){
      activeIndex.value = 0
    }
    else{
      activeIndex.value++
    }
  }

  let timerId = null;

  const startSlideShow = function(){
    timerId = setInterval(incrementActiveIndex, 2500)
  }

  const stopSlideShow = function(){
    clearInterval(timerId)
  }
 
  onMounted(() => {
    startSlideShow()
  })

  onUnmounted(() =>{
    stopSlideShow()
  })
</script>

<template>
  <h4>Vue Image Carousel</h4>
  <!----Thumbnail Design-----> 
  <ol class="carousel-thumnails">
    <img class="mx-1" :src="thumnail.image" v-for="(thumnail, index) in carouselItems" :key="index"  alt="" @click="activeIndex = index" height="60" :style="activeIndex != index?imageFilter:''" style="cursor: pointer;"> 
  </ol>
  <div @mouseover="stopSlideShow" @mouseleave="startSlideShow" id="carouselExampleCaptions" class="carousel">  
    <!----Indicator Design----->  
    <ol class="carousel-indicators">
      <li @click="activeIndex = index" v-for="(items, index) in carouselItems" :key="index" :class="index == activeIndex?'active':''"></li>
    </ol>
    
    <div class="carousel-inner">        
      <div class="carousel-item active">           
        <img height="600" :src="carouselItems[activeIndex].image" class="d-block w-100 img img-responsive" alt="...">
        <div class="carousel-caption d-none d-md-block">
          <h5>{{ carouselItems[activeIndex].title }}</h5>
          <p>{{ carouselItems[activeIndex].caption }}</p>
        </div>
      </div>  
    </div>    
    <a @click.prevent="0 == activeIndex ? activeIndex = (carouselItems.length) - 1 : activeIndex--" class="carousel-control-prev" href="#" role="button">
      <span class="carousel-control-prev-icon" aria-hidden="true"></span>
      <span class="sr-only">Previous</span>
    </a>
    <a @click.prevent="(carouselItems.length) - 1 == activeIndex ? activeIndex = 0 : activeIndex++" class="carousel-control-next" href="#" role="button">
      <span class="carousel-control-next-icon" aria-hidden="true"></span>
      <span class="sr-only">Next</span>
    </a>
  </div>
</template>

<style>
</style>