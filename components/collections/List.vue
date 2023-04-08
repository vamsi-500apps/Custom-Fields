<template>
  <div class="px-4 sm:px-6 lg:px-8 p-5">
    <div class="sm:flex sm:items-center">
      <div class="sm:flex-auto">
        <h1 class="text-base font-semibold leading-6 text-blue-900">
          Custom Fields
        </h1>
      </div>
      <div class="mt-4 sm:ml-16 sm:mt-0 sm:flex-none">
        <button
          @click="AddCustomField"
          type="button"
          class="block rounded-md bg-indigo-600 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
        >
          Add Custom Field
        </button>
      </div>
    </div>
    <div class="mt-8 flow-root">
      <div class="-mx-4 -my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
        <div class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8">
          <table class="min-w-full divide-y divide-gray-300">
            <thead>
              <tr>
                <th
                  scope="col"
                  class="whitespace-nowrap py-3.5 pl-4 pr-3 text-left text-sm font-semibold text-gray-900 sm:pl-0"
                >
                  Field Name
                </th>
                <th
                  scope="col"
                  class="whitespace-nowrap px-2 py-3.5 text-left text-sm font-semibold text-gray-900"
                >
                  Type
                </th>
                <th
                  scope="col"
                  class="whitespace-nowrap px-2 py-3.5 text-left text-sm font-semibold text-gray-900"
                >
                  Description
                </th>
                <th
                  scope="col"
                  class="whitespace-nowrap px-2 py-3.5 text-left text-sm font-semibold text-gray-900"
                >
                  Place Holder
                </th>
               
              </tr>
            </thead>
            <tbody class="divide-y divide-gray-200 bg-white">
              <tr v-for="(item,index) in CustomData" :key="index">
                <td
                  class="whitespace-nowrap py-2 pl-4 pr-3 text-sm text-gray-500 sm:pl-0"
                >
                  {{ item.name }}
                </td>
                <td
                  class="whitespace-nowrap px-2 py-2 text-sm font-medium text-gray-900"
                >
                  {{ item.type }}
                </td>
               
                <td class="whitespace-nowrap px-2 py-2 text-sm text-gray-500">
                  {{ item.type_data.description }}
                </td>
               
                <td
                  class="whitespace-nowrap px-2 py-2 text-center text-sm text-gray-500"
                >
                  {{ item.type_data.placeholder }}
                </td>
                <td
                  class="relative whitespace-nowrap py-2 pl-3 pr-4 text-right text-sm font-medium sm:pr-0"
                ></td>
                <td class="py-3 pr-6 whitespace-nowrap text-sm ">
                <button  @click="editData(item,index)">edit</button>
              </td>
               
              <td class="py-3 pr-6 whitespace-nowrap text-sm ">
                <button  @click="deleteData(item,index)">delete</button>
              </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup lang="ts">
import { defineProps, defineEmits } from "vue";
import { TrashIcon } from "@heroicons/vue/24/outline";

const props = defineProps({
  CustomData: {
    type: Array,
  },

});
const emit = defineEmits(["slideout","deleteDataItem","editDataItem",]);

//open sidebar for Add
const AddCustomField = () => {
  emit("slideout",);
  
};
const deleteData = (item: any, index: any) => {
  emit("deleteDataItem", item,index);
};
//Open Slidebar for Edit
const editData=(item:any,index:any)=>{
  console.log("item",item)
  emit("editDataItem",item);

}
</script>
