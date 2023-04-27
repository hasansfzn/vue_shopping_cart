<script setup>
import { onMounted, ref, reactive } from "vue";

const count = ref(0);

const incr = () => {
  count.value++;
};

onMounted(() => {
  console.log(`The initial count is ${count.value}`);
});

const rawHtml = `<span style="color:red">This is Inner</span>`;

const state = reactive({ cnt_num: 0 });

const incr_fun = () => {
  state.cnt_num++;
};

const rct_state = reactive({
  nested: { cnt_rct: 0 },
  arr: ["Reactive", "Vue", "Component"],
});

const muteDepply = () => {
  rct_state.nested.cnt_rct++;
  rct_state.arr.push(`Vue ${rct_state.nested.cnt_rct}`);
};
</script>

<template>
  <button class="btn_class" @click="incr">Count is : {{ count }}</button>
  <!-- to check v-html  -->
  <p>Using Text Braces: {{ rawHtml }}</p>
  <p>Using V-HTML: <span v-html="rawHtml"></span></p>
  <!-- reactive state  -->
  <h2 class="center">The below Count is Reactive</h2>
  <button class="btn_class" @click="incr_fun">{{ state.cnt_num }}</button>
  <!-- reactive state  nested-->
  <h2 class="center">Reactive Nested</h2>
  <button class="btn_class" @click="muteDepply">
    {{ rct_state.nested.cnt_rct }}
  </button>
</template>

<style scoped>
.btn_class {
  background-color: whitesmoke;
  border-radius: 5px;
}
.red {
  color: tomato;
  text-align: center;
}
.center {
  text-align: center;
  color: tomato;
  font-size: 1.2rem;
  padding: 20px;
}
</style>
