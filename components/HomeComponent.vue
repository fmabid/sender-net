<template>
  <div class="relative flex items-top min-h-screen bg-gray-100 sm:pt-0">
    <modal-component
      :show="showModal"
      @onSelect="hideModal"
      @onStart="handleData"
    />
    <div class="w-full p-16">
      <!-- Header -->
      <div class="flex flex-row items-center justify-between">
        <p class="font-semibold text-2xl">Sorting Training System</p>
        <!-- <button
          class="py-2 px-6 rounded text-white text-sm bg-[#FF8D00]"
          @click="sort"
        >
          Sort
        </button> -->

        <p v-if="endSorting" class="text-[#FF8D00] text-xl">
          You took <span class="text-green-500">{{ timeDiff }}</span> min to
          sort
        </p>

        <button
          class="py-2 px-6 rounded text-white text-sm bg-[#FF8D00]"
          @click="startSorting"
        >
          Start Sorting
        </button>
      </div>
      <!-- Header -->

      <div class="flex flex-col rounded shadow-md border mt-10">
        <div class="flex flex-row px-10 w-auto py-5 relative">
          <p class="ml-auto">{{ inputNum }} people in thins list</p>
        </div>

        <div class="block relative">
          <div class="relative overflow-x-auto">
            <table class="w-full table-fixed">
              <thead>
                <tr class="text-gray-500 text-left">
                  <th
                    class="
                      w-80
                      border-t border-b border-gray-300
                      px-4
                      py-2
                      font-light
                    "
                  >
                    Email
                  </th>
                  <th
                    class="
                      border border-r-0 border-gray-300
                      px-4
                      py-2
                      font-light
                    "
                  >
                    Potatoes
                  </th>
                  <th
                    class="
                      border-t border-b border-gray-300
                      px-4
                      py-2
                      font-light
                    "
                  >
                    Tags
                  </th>
                  <th
                    class="
                      border-t border-b border-gray-300
                      px-4
                      py-2
                      font-light
                    "
                  >
                    Full name
                  </th>
                  <th
                    class="
                      border-t border-b border-gray-300
                      px-4
                      py-2
                      font-light
                    "
                  >
                    Location
                  </th>
                </tr>
              </thead>

              <draggable
                v-model="people"
                tag="tbody"
                class="text-gray-700 font-normal text-base"
                @change="checkSorting"
              >
                <tr v-for="indivis in people" :key="indivis.id">
                  <td class="border-t border-b border-gray-300 px-4 py-2">
                    <div
                      class="
                        flex flex-rows
                        items-center
                        justify-between
                        space-x-2
                      "
                    >
                      <div class="flex flex-row items-center space-x-4">
                        <input type="checkbox" name="" />

                        <p>{{ indivis.email }}</p>
                      </div>

                      <icon-chevron-right class="w-4" />
                    </div>
                  </td>
                  <td class="border border-r-0 border-gray-300 px-4 py-2">
                    {{ indivis.potatoes }}
                  </td>
                  <td class="border-t border-b border-gray-300 px-4 py-2">
                    <tag v-if="indivis.tags" :tag-name="indivis.tags" />
                  </td>
                  <td class="border-t border-b border-gray-300 px-4 py-2">
                    {{ indivis.name }}
                  </td>
                  <td class="border-t border-b border-gray-300 px-4 py-2">
                    {{ indivis.location }}
                  </td>
                </tr>
              </draggable>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import draggable from 'vuedraggable'
import IconChevronRight from './icons/IconChevronRight.vue'
import ModalComponent from './ModalComponent.vue'
import Tag from './utility/Tag.vue'

export default {
  components: { IconChevronRight, Tag, draggable, ModalComponent },
  data() {
    return {
      people: [],
      sortedList: [],
      inputNum: 0,
      startTime: null,
      endTime: null,
      timeDiff: null,

      // flags
      showModal: false,
      endSorting: false,
    }
  },
  methods: {
    getRandomData() {
      this.$axios
        .$get('https://my.api.mockaroo.com/ptatopeople.json?key=96f23b40')
        .then((resp) => {
          this.people = resp.slice(0, this.inputNum)

          this.startTime = Date.now()
          this.people.forEach((element) => {
            element.potatoes = Math.floor(Math.random() * 10000) + 1
          })
          this.sort()
        })
    },
    sort() {
      this.sortedList = [...this.people]
      this.sortedList.sort((a, b) => a.potatoes - b.potatoes)
    },
    startSorting() {
      this.toggleModal()
    },
    toggleModal() {
      this.showModal = !this.showModal
    },
    hideModal() {
      this.showModal = false
    },
    handleData(v) {
      if (v) {
        this.showModal = false
        this.inputNum = parseInt(v)
        this.getRandomData()
      }
    },
    checkSorting() {
      if (this.isEqual(this.people, this.sortedList)) {
        this.endSorting = true
        this.endTime = Date.now()
        this.timeDiff = (this.endTime - this.startTime) / (1000 * 60) // min
      }
    },
    isEqual(a, b) {
      return JSON.stringify(a) === JSON.stringify(b)
    },
  },
}
</script>

<style scoped></style>
