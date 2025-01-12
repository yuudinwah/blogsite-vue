<template>
  <header :class="['fixed bg-white shadow-lg fixed w-screen h-20 z-10', className]">
    <nav class="mx-auto flex max-w-7xl items-center justify-between p-6 lg:px-8" aria-label="Global">
      <div class="flex lg:flex-1">
        <a href="/" class="-m-1.5 p-1.5">
          My Blog
        </a>
      </div>
      <div class="flex">
        <button
          type="button"
          class="-m-2.5 inline-flex items-center justify-center rounded-md p-2.5 text-gray-700"
          @click="toggleOpen"
        >
          <span class="sr-only">Open main menu</span>
          <svg
            class="size-6"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            aria-hidden="true"
            data-slot="icon"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5"
            />
          </svg>
        </button>
      </div>
    </nav>

    <div :class="{ hidden: !open }" role="dialog" aria-modal="true">
      <div class="fixed inset-0 z-10"></div>
      <div
        class="fixed inset-y-0 right-0 z-10 w-full overflow-y-auto bg-white px-6 py-6 sm:max-w-sm sm:ring-1 sm:ring-gray-900/10"
      >
        <div class="flex items-center justify-between">
          <a href="#" class="-m-1.5 p-1.5">
            <span class="sr-only">Your Company</span>
            <img
              class="dark:invert"
              src="/icon-192.png"
              alt="logo"
              width="50"
              height="50"
            />
          </a>
          <button
            type="button"
            class="-m-2.5 rounded-md p-2.5 text-gray-700"
            @click="toggleOpen"
          >
            <span class="sr-only">Close menu</span>
            <svg
              class="size-6"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              aria-hidden="true"
              data-slot="icon"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M6 18 18 6M6 6l12 12"
              />
            </svg>
          </button>
        </div>
        <div class="mt-6 flow-root">
          <div class="-my-6 divide-y divide-gray-500/10">
            <div class="space-y-2 py-6">
              <!-- Add HeaderMenuComponent here -->
            </div>
            <div class="py-6">
              <HeaderMenuComponent
                content="Log in"
                action="/dashboard"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
  </header>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'
import HeaderMenuComponent from './headerMenu.vue'

interface Props {
  className?: string
}

export default defineComponent({
  name: 'HeaderComponent',
  components: {
    HeaderMenuComponent
  },
  props: {
    className: {
      type: String,
      default: ''
    }
  },
  setup() {
    const open = ref(false)

    const toggleOpen = () => {
      open.value = !open.value
    }

    return {
      open,
      toggleOpen
    }
  }
})
</script>

<!-- Atau menggunakan <script setup> -->
<!--
<script setup lang="ts">
import { ref } from 'vue'
import HeaderMenuComponent from './HeaderMenu.vue'

interface Props {
  className?: string
}

defineProps<Props>()

const open = ref(false)

const toggleOpen = () => {
  open.value = !open.value
}
</script>
-->
