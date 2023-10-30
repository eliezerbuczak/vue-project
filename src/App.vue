<template>
  <div class="w-full flex h-screen items-center justify-center relative">
    <div class="wrapper bg-orange-600 h-auto w-96">
      <header class="cursor-move" @mousedown="startDrag(1)" @mouseup="stopDrag(1)">Draggable Div 1</header>
      <div class="content">
        <div class="icon"></div>
        <div class="title">Draggable Div 1</div>
        <p>This is a draggable div which is created using HTML CSS & JavaScript. You can move this div anywhere on the document or page.</p>
      </div>
    </div>

    <div class="wrapper bg-blue-600 h-auto w-96" >
      <header class="cursor-move" @mousedown="startDrag(2 )" @mouseup="stopDrag(2)">Draggable Div 2</header>
      <div class="content">
        <div class="icon"></div>
        <div class="title">Draggable Div 2</div>
        <p>This is another draggable div. You can move this one too!</p>
      </div>
    </div>
    <div class="wrapper bg-green-400 h-auto w-96">
      <header class="cursor-move" @mousedown="startDrag(3 )" @mouseup="stopDrag(3)">Draggable Div 2</header>
      <div class="content">
        <div class="icon"></div>
        <div class="title">Draggable Div 2</div>
        <p>This is another draggable div. You can move this one too!</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

let isDragging = false;
let activeWrapper = null;

const startDrag = (wrapperId) => {
  if (!isDragging) {
    isDragging = true;
    activeWrapper = wrapperId;
    document.querySelector(`.wrapper${wrapperId}`).classList.add("active");
    document.addEventListener("mousemove", onDrag);
  }
};

const stopDrag = (wrapperId) => {
  if (activeWrapper === wrapperId) {
    isDragging = false;
    activeWrapper = null;
    document.querySelector(`.wrapper${wrapperId}`).classList.remove("active");
    document.removeEventListener("mousemove", onDrag);
  }
};

const onDrag = (event) => {
  if (isDragging) {
    const movementX = event.movementX;
    const movementY = event.movementY;
    let element = document.querySelector(`.wrapper${activeWrapper}`);
    let getStyle = window.getComputedStyle(element);
    let leftVal = parseInt(getStyle.left);
    let topVal = parseInt(getStyle.top);
    element.style.left = `${leftVal + movementX}px`;
    element.style.top = `${topVal + movementY}px`;
  }
};

onMounted(() => {
  document.querySelectorAll(".wrapper").forEach((element, index) => {
    element.style.position = "absolute";
    element.classList.add(`wrapper${index + 1}`);
  });
});
</script>
