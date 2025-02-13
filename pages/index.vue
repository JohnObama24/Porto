<script setup>
import { ref, onMounted } from "vue";
import gsap from "gsap";


const text = ref("Hii, I am Frontend And Indie Game dev");
const textContainer = ref(null);

onMounted(() => {
  const letters = textContainer.value.querySelectorAll(".letter");

  gsap.fromTo(
    letters,
    { opacity: 0, y: 20 },
    {
      opacity: 1,
      y: 0,
      stagger: 0.05, // Jeda antar huruf iya kali, lupa guaa
      duration: 2.0,
      ease: "power3.out",
    }
  );
});
</script>



<template>
 <div ref="textContainer" class="text-7xl font-semibold text-center break-words whitespace-normal">
    <span v-for="(letter, index) in text.split('')" :key="index" class="letter text-wrap">
  {{ letter === ' ' ? '\u00A0' : letter }}
</span>

  </div>
</template>

<style scoped>
.letter {
  display: inline-block;
}

.text-container {
  white-space: pre;
}

</style>