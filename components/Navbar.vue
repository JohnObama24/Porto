<template>
  <nav class="w-full h-20 px-4 py-20  flex flex-col items-center justify-center fixed">
    <div class="max-w-7xl mx-auto flex w-full items-center justify-between">
      <div class="text-black text-2xl font-bold">OBAMA</div>
      <ul class="flex gap-4" v-if="!isScrool">
        <li
          class="nav-item relative rotate-90 cursor-pointer flex items-center  text-black font-semibold w-fit"
        >
          <span>Home</span>
        </li>
        <li
          class="nav-item relative rotate-90 cursor-pointer flex items-center  text-black font-semibold w-fit"
        >
          <span>About</span>
        </li>
        <li
          class="nav-item relative rotate-90 cursor-pointer flex items-center  text-black font-semibold w-fit"
        >
          <span>Project</span>
        </li>
        <li
          class="nav-item relative rotate-90 cursor-pointer flex items-center  text-black font-semibold w-fit"
        >
          <span>More</span>
        </li>
      </ul>
      <button v-if="isScrool">Menu</button>
    </div>
  </nav>
</template>

<script lang="js" setup>
import { onMounted } from "vue";
import { gsap } from "gsap";
import { SplitText } from "gsap/SplitText";

const isScrool = ref(false)

gsap.registerPlugin(SplitText);

function HoverNav() {
  const elementHover = document.querySelectorAll(".nav-item");

  elementHover.forEach((element) => {
    const original = element.querySelector("span");
    const clonedText = original.cloneNode(true);
    element.appendChild(clonedText);

    gsap.set(clonedText, {
      position: "absolute",
      top: 0,
      left: 0
    });

    const OriSplit = new SplitText(original, { type: "chars" });
    const CloneSplit = new SplitText(clonedText, { type: "chars" });

    gsap.set(CloneSplit.chars, {
      rotationX: -20,
      opacity: 0,
      transformOrigin: "50% 50% -50",
    });

    const stagger = { each: 0.05, ease: "power2", from: "start" };

    const tl = gsap.timeline({ paused: true });

    tl.to(OriSplit.chars, {
      duration: 0.5,
      rotationX: 30,
      transformOrigin: "50% 50% -45",
      stagger: stagger
    });

    tl.to(OriSplit.chars, {
      duration: 0.2,
      opacity: 0,
      stagger: stagger,
      ease: "power3.in"
    }, 0);

    tl.to(CloneSplit.chars, {
      duration: 0.05,
      opacity: 1,
      stagger: stagger,
    }, 0.001);

    tl.to(CloneSplit.chars, {
      duration: 0.4,
      rotationX: 0,
      stagger: stagger,
    }, 0);

    element.addEventListener("mouseenter", () => {
      tl.restart();
    });

    element.addEventListener("mouseleave", () => {
      tl.reverse();
    });
  });
}

const HandleScroll = () => {
  isScrool.value = window.scrollY > 10
}


onMounted(() => {
  HoverNav();

  window.addEventListener('scroll', HandleScroll);
});
</script>

<style scoped></style>
