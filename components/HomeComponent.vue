<!-- Please remo
  components: { IconChevronRight },ve this file from your project -->
<template>
  <div class="relative flex items-top min-h-screen bg-gray-100 sm:pt-0">
    <div class="w-full p-16">
      <div class="flex flex-row items-center justify-between">
        <p class="font-semibold text-2xl">Sorting Training System</p>

        <button class="py-2 px-6 rounded text-white text-sm bg-[#FF8D00]">
          Start Sorting
        </button>
      </div>

      <div class="flex flex-col rounded shadow-md border mt-10">
        <div class="flex flex-row px-10 w-auto py-5 relative">
          <p class="ml-auto">20 people in thins list</p>
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

              <tbody class="text-gray-700 font-normal text-base">
                <tr v-for="i in 10" :key="i">
                  <td class="border-t border-b border-gray-300 px-4 py-2">
                    <div
                      class="
                        flex flex-row
                        items-center
                        justify-between
                        space-x-2
                      "
                    >
                      <div class="flex flex-row items-center space-x-4">
                        <input type="checkbox" name="" />

                        <p>dsdcs@mail.com</p>
                      </div>

                      <icon-chevron-right class="w-4" />
                    </div>
                  </td>
                  <td class="border border-r-0 border-gray-300 px-4 py-2">
                    Adam
                  </td>
                  <td class="border-t border-b border-gray-300 px-4 py-2">
                    858
                  </td>
                  <td class="border-t border-b border-gray-300 px-4 py-2">
                    858
                  </td>
                  <td class="border-t border-b border-gray-300 px-4 py-2">
                    858
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import IconChevronRight from './IconChevronRight.vue'

export default {
  components: { IconChevronRight },
}
</script>

<style scoped></style>
