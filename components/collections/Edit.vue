  <template>

    <TransitionRoot as="template" :show="open">
      <Dialog as="div" class="relative z-10" @close="open = false">
        <TransitionChild as="template" enter="ease-out duration-300" enter-from="opacity-0" enter-to="opacity-100" leave="ease-in duration-200" leave-from="opacity-100" leave-to="opacity-0">
          <div class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity" />
        </TransitionChild>
  
        <div class="fixed inset-0 z-10 overflow-y-auto">
          <div class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0">
            <TransitionChild as="template" enter="ease-out duration-300" enter-from="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95" enter-to="opacity-100 translate-y-0 sm:scale-100" leave="ease-in duration-200" leave-from="opacity-100 translate-y-0 sm:scale-100" leave-to="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95">
              <DialogPanel class="relative transform overflow-hidden rounded-lg bg-white px-4 pb-4 pt-5 text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg sm:p-6">
                <div>
                  <div class="mx-auto flex h-12 w-12 items-center justify-center rounded-full bg-green-100">
                    <CheckIcon class="h-6 w-6 text-green-600" aria-hidden="true" />
                  </div>
                  <lable>Field name</lable>
                  <input open="true"
          v-model="field_name"
          property="value"
          type="text"
          class="block mb-3 px-3 rounded-md border-0 py-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[90%]"
          placeholder="enter custom field name"
        />
        <lable>Type</lable>
                  <select open="true"
          v-model="type"
          property="value"
          type="text"
          class="block mb-3 px-3 rounded-md border-0 py-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[90%]"
          placeholder="select type"
        >
      <option value="textarea">TextArea</option>
      <option value="list">LIST</option>
      <option value="textbox">TextBox</option>
      <option value="radio">Radio Buttons</option>
      <option value="multi">Multi Checkbox</option>
      
    </select>
        <lable>Description</lable>
                  <input open="true"
          v-model="description"
          property="value"
          type="text"
          class="block mb-3 px-3 rounded-md border-0 py-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[90%]"
          placeholder="enter description"
        />
        <lable>Place Holder</lable>
                  <input open="true"
          v-model="placeholder"
          property="value"
          type="text"
          class="block mb-3 px-3 rounded-md border-0 py-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[90%]"
          placeholder="enter place holder"
        />
  
     
                </div>
                <div class="mt-5 sm:mt-6 sm:grid sm:grid-flow-row-dense sm:grid-cols-2 sm:gap-3">
                  <button type="button" class="inline-flex w-full justify-center rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 sm:col-start-2" @click="editData()">save</button>
                  <button type="button" class="mt-3 inline-flex w-full justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50 sm:col-start-1 sm:mt-0" @click="open = false" ref="cancelButtonRef">Cancel</button>
                </div>
              </DialogPanel>
            </TransitionChild>
          </div>
        </div>
      </Dialog>
    </TransitionRoot>
  </template>
  <script setup lang="ts">
  import { ref, defineEmits, defineProps } from "vue";
  import {
    Dialog,
    DialogPanel,
    DialogTitle,
    TransitionChild,
    TransitionRoot,
  } from "@headlessui/vue";
  
  const emit = defineEmits(["customEditemit"]);
  const props = defineProps({
    data: {
      type: Object,
    },
  });
  //console.log("=========>propssss",props.data.name)
  let field_name = ref(props.data.name);
  let type = ref(props.data.type);
  let description = ref(props.data.type_data.description);
  let placeholder = ref(props.data.type_data.placeholder);
  const open = ref(true);
  //Sending body through the emit
  const editData = async () => {
    let body = {
      name: field_name.value,
      type: type.value,
      entity: "CONTACTS",
      type_data: {
        is_required: 1,
        show_in_filter: 1,
        length: 100,
        description: description.value,
        placeholder: placeholder.value,
      },
      uid: props.data.uid,
    };
    emit("customEditemit", body);
    open.value=false;
  };
  </script>  
  <!-- <template></template> --> 