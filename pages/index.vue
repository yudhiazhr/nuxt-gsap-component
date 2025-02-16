<script setup>
import { onMounted } from 'vue';
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

// Register ScrollTrigger
gsap.registerPlugin(ScrollTrigger);

onMounted( () => {
  gsap.fromTo(
    ".containerElement",
    { width: "90%", height: "90%", borderRadius: 30 },
    {
      width: "100%", height: "100%", borderRadius: 0,
      scrollTrigger: {
        trigger: ".section2",
        start: "top 70%",
        end: "bottom 70%", 
        scrub: 1,
        markers: true,
        id: "expand",
      }
    }
  );

  gsap.timeline({
    scrollTrigger: {
      trigger: ".section2",
      start: "top top",
      end: "bottom",
      pin: true,
      scrub: 1,
      markers: true,
      id: "pin-section2",
    },
  })

  .fromTo(".image", { scale: 1 }, { scale: 0.25 }, "<")
  .fromTo(".image", { opacity: 1 }, { opacity: 0 })
  .fromTo(".items h1",
    { opacity: 0, x: 0 },
    { opacity: 1, x: (index) => (index - 1) * 600 }
  )
  .to(".containerElement", { backgroundColor: "rgba(32, 84, 250, 0.5)" })
  .fromTo(
    ".containerElement",
    { width: "100%", height: "100%", borderRadius: 0 },
    {
      width: "90%", height: "90%", borderRadius: 30,
      scrollTrigger: {
        trigger: ".section3",
        start: "top 90%",
        end: "bottom 90%", 
        scrub: 1,
        markers: true,
        id: "shrink",
      }
    }
  );

  const images = document.querySelectorAll(".background-images img");

  gsap.set(images, { opacity: 0 });

  let imgTl = gsap.timeline({ repeat: -1 });

  images.forEach((img, i) => {
    imgTl.to(img, { opacity: 1, duration: 1 })
        .to(img, { opacity: 1, duration: 1 }, "+=1");
  });
});
</script>

<template>
  <section id="section1" class="pt-44 pb-32 px-12 flex items-center">
    <h1 class="title w-1/2 text-[130px] leading-[100%] text-[#2054FA]">
      Web Bring Your Brand to Life
    </h1>
  </section>

  <section id="section2" class="section2 flex justify-center items-center w-full h-dvh relative overflow-hidden">
    <div class="containerElement relative flex justify-center items-center bg-[#2054FA] w-[90%] h-[90%] text-white overflow-hidden">
      <img class="absolute image" src="/assets/Group 7.png" alt="Animated Image">
      <div class="items relative justify-evenly items-center w-full flex">
        <h1 class="text-6xl absolute">Agency</h1>
        <h1 class="text-6xl absolute">Laboratory</h1>
        <h1 class="text-6xl absolute">Engine</h1>
      </div>
      <div class="absolute z-[-1] flex w-full h-full overflow-hidden background-images">
        <img class="w-full absolute"  src="/assets/RB.png" alt="">
        <img class="w-full absolute"  src="/assets/Bags.png" alt="">
        <img class="w-full absolute"  src="/assets/chair.png" alt="">
        <img class="w-full absolute"  src="/assets/concert.png" alt="">
      </div>
    </div>
  </section>

  <section id="section3" class="section3 flex justify-center items-center w-full min-h-dvh bg-white relative">
  </section>
</template>