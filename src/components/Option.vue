<template>
  <div class="flex flex-col mx-10">
    <label class="">{{ place }} </label>
    <br />
    <select class="cursor-pointer" v-model="selectArray">
      <option
        v-for="(array, index) in arrays"
        :key="index"
        :value="array[keyName]"
      >
        {{ array[titleName] }}
      </option>
    </select>
  </div>
</template>

<script setup>
import { ref, watch, reactive } from "vue";
const emit = defineEmits(["send:data"]);
const props = defineProps({
  arrays: Object,
  place: String,
  keyName: Object,
  titleName: Object,
});

const selectArray = ref("");
function sendDataToParent() {
  emit("send:data", selectArray.value);
}
watch(selectArray, (newValue, oldValue) => {
  sendDataToParent();
});
</script>
<!-- const Mehrzad = reactive([...props.arrays]); -->
