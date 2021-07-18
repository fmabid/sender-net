<template>
  <div class="modal" :class="[show ? 'block' : 'hidden']">
    <!-- Modal content -->
    <!-- <div class="w-10/12 sm:w-2/5 text-center modal-content">
      <p class="text-lg pb-6">
        {{ msg }}
      </p>

      <div class="space-x-8">
        <button class="btn btn-yes" @click.prevent="onEmitValue">Close</button>

        <button class="btn btn-no" @click.prevent="onEmitValue(false)">
          No
        </button>
      </div>
    </div> -->
    <div class="w-10/12 sm:w-2/5 mx-auto bg-white rounded-md">
      <div class="relative divide-y divide-gray-300">
        <div class="flex items-center justify-between p-5">
          <p class="text-lg font-semibold">How many people?</p>

          <cancle
            class="text-gray-500 cursor-pointer"
            @click.native="onHideModal"
          />
        </div>

        <div class="px-5 pt-6 pb-10">
          <p class="mb-5">
            Enter a number of how many people you want to add to the list.
          </p>

          <input
            v-model="input"
            class="
              outline-none
              w-full
              text-sm text-black
              placeholder-gray-500
              border border-gray-200
              rounded-md
              py-2
              px-4
            "
            type="number"
          />
          <span v-if="err" class="text-red-700 text-xs"
            >Number must be between 20 to 100</span
          >
        </div>

        <div class="p-5 relative flex">
          <div class="space-x-3 ml-auto">
            <button
              class="bg-gray-300 px-8 py-2 rounded-md text-gray-600"
              @click="onHideModal"
            >
              Cancle
            </button>

            <button
              class="px-8 py-2 rounded-md text-white bg-[#FF8D00]"
              @click="onEmitValue"
            >
              Start
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Cancle from './icons/Cancle.vue'
export default {
  components: {
    Cancle,
  },
  props: {
    show: {
      default: false,
      type: Boolean,
    },
  },
  data() {
    return {
      input: null,
      err: false,
    }
  },
  methods: {
    onHideModal() {
      this.$emit('onSelect')
    },
    onEmitValue() {
      if (this.input < 20 || this.input > 100) {
        this.err = true
        return
      }
      this.$emit('onStart', this.input)
    },
  },
}
</script>

<style>
.modal {
  position: fixed; /* Stay in place */
  z-index: 1; /* Sit on top */
  padding-top: 100px; /* Location of the box */
  left: 0;
  top: 0;
  width: 100%; /* Full width */
  height: 100%; /* Full height */
  overflow: auto; /* Enable scroll if needed */
  background-color: rgb(0, 0, 0); /* Fallback color */
  background-color: rgba(0, 0, 0, 0.4); /* Black w/ opacity */
}
</style>
