<template>
  <button class="view-btn">
    <svg
      xmlns="http://www.w3.org/2000/svg"
      width="22"
      height="22"
      viewBox="0 0 16 16"
      fill="none"
      stroke="#00bfff"
      stroke-width="1.5"
    >
      <path
        d="M1 8s3-5 7-5 7 5 7 5-3 5-7 5-7-5-7-5z"
        stroke-linecap="round"
        stroke-linejoin="round"
      />
      <circle cx="8" cy="8" r="2.5" stroke-linecap="round" stroke-linejoin="round" />
      <circle cx="8" cy="8" r="1" fill="#00bfff" />
    </svg>
  </button>
</template>

<script setup></script>

<style>
.view-btn {
  border: none;
  background-color: transparent;
  cursor: pointer;
  border-radius: 4px;
}

.view-btn svg {
  transition:
    transform 0.25s ease,
    stroke 0.25s ease;
}

.view-btn:hover svg {
  stroke: #0056b3;
  transform: scale(1.2);
}
</style>
