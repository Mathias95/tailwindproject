<template>
    <div class="relative">
        <button @click="toggle" @focus="buttonHasFocus = true" @blur="buttonHasFocus = false" type="button" class="block focus:outline-none">
            <slot name="trigger" :hasFocus="buttonHasFocus" :isOpen="isOpen"></slot>
        </button>
        <div :class="[isOpen ? 'block' : 'hidden']">
            <button @click="isOpen = false" type="button" class="z-30 block fixed opacity-0 inset-0 cursor-default w-full h-full focus:outline-none"></button>
            <div class="z-40 absolute right-0">
                <slot name="dropdown"></slot>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: [],
    data() {
        return {
            buttonHasFocus: false,
            isOpen: false,
        }
    }, 
    mounted(){
      const onEscape = (e) => {
        if (!this.isOpen || e.key !== 'Escape') {
          return
        }
        this.isOpen = false
      }
      document.addEventListener('keydown', onEscape)
      this.$on('hook:destroyed', () => {
        document.removeEventListener('keydown', onEscape)
      })
    },
    methods: {
        toggle(){
            this.isOpen =!this.isOpen
        },
    },
}
</script> 
