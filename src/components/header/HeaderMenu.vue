<template>
  <div class="-mx-3 lg:relative">
    <button 
      type="button" 
      class="lg:flex lg:items-center lg:gap-x-1 lg:text-sm/6 lg:font-semibold lg:text-gray-900 flex w-full items-center justify-between rounded-lg py-2 pl-3 pr-3.5 text-base/7 font-semibold text-gray-900 hover:bg-gray-50" 
      aria-controls="disclosure-1" 
      aria-expanded="false"
      @click="handleButtonClick"
    >
      {{ content }}

      <svg 
        :class="['size-5 flex-none text-gray-400', { 'hidden': !subMenus }]" 
        viewBox="0 0 20 20" 
        fill="currentColor" 
        aria-hidden="true" 
        data-slot="icon"
      >
        <path 
          fill-rule="evenodd" 
          d="M5.22 8.22a.75.75 0 0 1 1.06 0L10 11.94l3.72-3.72a.75.75 0 1 1 1.06 1.06l-4.25 4.25a.75.75 0 0 1-1.06 0L5.22 9.28a.75.75 0 0 1 0-1.06Z" 
          clip-rule="evenodd" 
        />
      </svg>
    </button>
    <div :class="[
      'lg:absolute lg:-left-8 lg:top-full lg:z-10 lg:mt-3 lg:w-screen lg:max-w-md lg:overflow-hidden lg:flex-auto lg:pl-16 pl-8',
      { 'hidden': !open }
    ]">
      <slot></slot>
      <template v-if="subMenus">
        <HeaderMenuComponent
          v-for="(item, index) in subMenus"
          :key="index"
          v-bind="item"
        />
      </template>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'
import { useRouter } from 'vue-router'

interface HeaderMenuInterface {
  content: string
  action?: string | (() => void)
  subMenus?: HeaderMenuInterface[]
}

export default defineComponent({
  name: 'HeaderMenuComponent',
  props: {
    content: {
      type: String,
      required: true
    },
    action: {
      type: [String, Function],
      default: undefined
    },
    subMenus: {
      type: Array as () => HeaderMenuInterface[],
      default: () => []
    }
  },
  setup(props) {
    const open = ref(false)
    const router = useRouter()

    const handleAction = () => {
      if (!props.action) return

      if (typeof props.action === 'string') {
        router.push(props.action)
      } else {
        props.action()
      }
    }

    const handleButtonClick = () => {
      if (props.subMenus && props.subMenus.length > 0) {
        open.value = !open.value
      } else {
        handleAction()
      }
    }

    return {
      open,
      handleButtonClick
    }
  }
})
</script>

<!-- Atau menggunakan <script setup> -->
<!--
<script setup lang="ts">
import { ref } from 'vue'
import { useRouter } from 'vue-router'

interface HeaderMenuInterface {
  content: string
  action?: string | (() => void)
  subMenus?: HeaderMenuInterface[]
}

const props = defineProps<{
  content: string
  action?: string | (() => void)
  subMenus?: HeaderMenuInterface[]
}>()

const open = ref(false)
const router = useRouter()

const handleAction = () => {
  if (!props.action) return

  if (typeof props.action === 'string') {
    router.push(props.action)
  } else {
    props.action()
  }
}

const handleButtonClick = () => {
  if (props.subMenus && props.subMenus.length > 0) {
    open.value = !open.value
  } else {
    handleAction()
  }
}
</script>
-->
