<script setup>
import { nextTick, onMounted, ref, watch } from "vue";
import Draggable from "draggable";

const showModal = ref(false);
const weight = ref(50);
const modal1 = ref();
const modal2 = ref();
const modal2Draggable = ref();

const calculate = () => {
  showModal.value = true;
};

const closeResult = () => {
  showModal.value = false;
};

const nio = () => {
  alert("Noup");
};

watch(showModal, async () => {
  if (showModal.value) {
    await nextTick();

    modal2Draggable.value = new Draggable(modal2.value, {
      handle: modal2.value.querySelector("#modal2-header"),
      filterTarget: (target) => {
        return target.tagName !== "BUTTON" && target.closest("button") === null;
      },
    });
  } else {
    modal2Draggable.value.destroy();
  }
});

onMounted(() => {
  new Draggable(modal1.value, {
    handle: modal1.value.querySelector("#modal1-header"),
  });
});
</script>

<template>
  <div
    class="h-screen w-screen bg-gray-50 top-0 left-0 flex flex-col justify-end main bg-cover"
  >
    <div
      class="h-screen w-screen flex items-center justify-center absolute top-0 left-0"
    >
      <div
        ref="modal1"
        class="flex flex-col mx-auto border shadow bg-gray-100 z-10"
      >
        <div
          id="modal1-header"
          class="flex bg-white p-3 justify-between cursor-pointer"
        >
          <span class="flex space-x-2">
            <span>🥛</span>
            <span class="text-gray-600">Weight Calculator</span>
          </span>

          <button type="button" class="ml-auto text-gray-400" @click="nio">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-5 w-5"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M6 18L18 6M6 6l12 12"
              />
            </svg>
          </button>
        </div>

        <div class="p-5 flex flex-col space-y-4">
          <div class="flex space-x-2 text-gray-800 items-center">
            <label for="peso"> Introduce your weight </label>

            <input
              v-model="weight"
              type="number"
              class="border border-gray-200 px-3 py-1"
            />

            <span> kg </span>
          </div>

          <div class="flex justify-end">
            <button
              @click="calculate"
              type="button"
              class="border-gray-600 px-5 py-1 bg-gray-300 ml-auto hover:bg-gray-500 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500"
            >
              Calculate
            </button>
          </div>
        </div>
      </div>

      <div
        v-if="showModal"
        ref="modal2"
        class="flex flex-col mx-auto border shadow bg-gray-100 z-20"
      >
        <div id="modal2-header" class="flex bg-white p-3 flex-col space-y-4">
          <div class="flex justify-between">
            <span class="text-gray-600">Result</span>

            <button
              type="button"
              class="ml-auto text-gray-400"
              @click="closeResult"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                class="h-5 w-5"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M6 18L18 6M6 6l12 12"
                />
              </svg>
            </button>
          </div>
          <div class="p-5 space-x-10 flex items-center">
            <div class="text-blue-500">
              <svg
                xmlns="http://www.w3.org/2000/svg"
                class="h-14 w-14"
                viewBox="0 0 20 20"
                fill="currentColor"
              >
                <path
                  fill-rule="evenodd"
                  d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7 4a1 1 0 11-2 0 1 1 0 012 0zm-1-9a1 1 0 00-1 1v4a1 1 0 102 0V6a1 1 0 00-1-1z"
                  clip-rule="evenodd"
                />
              </svg>
            </div>

            <span>Your weight is {{ weight }} kg!</span>
          </div>
        </div>

        <div class="p-5 flex flex-col space-y-4">
          <div class="flex justify-end">
            <button
              @click="closeResult"
              type="button"
              class="border-gray-600 px-5 py-1 bg-gray-300 ml-auto hover:bg-gray-500 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500"
            >
              Accept
            </button>
          </div>
        </div>
      </div>
    </div>

    <div
      class="relative flex flex-col z-0 items-center justify-center pb-10 mx-auto space-y-3 text-sm text-center text-white sm:flex-row whitespace-nowrap sm:space-y-0"
    >
      <span class="inline-flex items-center px-3">
        Made with
        <svg
          viewBox="0 0 20 20"
          fill="currentColor"
          class="w-4 h-4 mx-1 text-red-300"
        >
          <path
            fill-rule="evenodd"
            d="M3.172 5.172a4 4 0 015.656 0L10 6.343l1.172-1.171a4 4 0 115.656 5.656L10 17.657l-6.828-6.829a4 4 0 010-5.656z"
            clip-rule="evenodd"
          ></path>
        </svg>
        by
        <a
          href="https://twitter.com/alfonsobries"
          target="_blank"
          class="ml-1 text-white underline"
          >Alfonso Bribiesca</a
        ></span
      >
      <a
        href="https://github.com/alfonsobries/calculadora-de-peso"
        target="_blank"
        class="inline-flex items-center px-3 text-white underline border-gray-200 sm:border-l"
        ><svg
          width="16"
          height="16"
          viewBox="0 0 16 16"
          fill="currentColor"
          class="w-4 h-4 mr-2"
        >
          <path
            d="M7.975 16a9.39 9.39 0 003.169-.509c-.473.076-.652-.229-.652-.486l.004-.572c.003-.521.01-1.3.01-2.197 0-.944-.316-1.549-.68-1.863 2.24-.252 4.594-1.108 4.594-4.973 0-1.108-.39-2.002-1.032-2.707.1-.251.453-1.284-.1-2.668 0 0-.844-.277-2.77 1.032A9.345 9.345 0 008 .717c-.856 0-1.712.113-2.518.34C3.556-.24 2.712.025 2.712.025c-.553 1.384-.2 2.417-.1 2.668-.642.705-1.033 1.612-1.033 2.707 0 3.852 2.342 4.72 4.583 4.973-.29.252-.554.692-.642 1.347-.58.264-2.027.692-2.933-.831-.19-.302-.756-1.045-1.549-1.032-.843.012-.34.478.013.667.428.239.919 1.133 1.032 1.422.201.567.856 1.65 3.386 1.184 0 .55.006 1.079.01 1.447l.003.428c0 .265-.189.567-.692.479 1.007.34 1.926.516 3.185.516z"
          ></path>
        </svg>
        Github Source
      </a>
      <a
        href="https://twitter.com/anamariasosam/status/1493991449859399682?s=20&t=IZeBS3qyBnrUGbQdxNeYMA"
        target="_blank"
        class="inline-flex items-center px-3 text-white underline border-gray-200 sm:border-l"
      >
        Based on this tweet 😂</a
      >
    </div>
  </div>
</template>
