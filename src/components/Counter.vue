<template>
  <div>
    <p id="alrt" v-if="test">{{ alrt }}</p>
    <input
      type="text"
      @input="test1"
      v-model="name"
      placeholder="Enter your name"
    />
    <button @click="show">ADDDDD</button>
    <button @click="clearall">Clear All</button>
    <p>Checked: {{ checkedCount }}</p>
    <p>Unchecked: {{ uncheckedCount }}</p>

    <draggable v-model="inview" item-key="text" tag="ul" :component-data="{
    tag: 'ul',
    type: 'transition-group',
    name: 'fade'
  }">
      <template #item="{ element, index }">
        <li @click="toggleCheck(index)" :class="{ checked: element.checked }">
          |{{ element.text }}|
          <button @click.stop="deleteItem(index)">❌</button>
        </li>
      </template>
    </draggable>
  </div>
</template>
<script setup>
import { ref, computed } from "vue";
import draggable from "vuedraggable";
const name = ref("");
const inview = ref([]);
const alrt = ref("Please enter at least 5 characters.");
const test = ref(false);
const test1 = () => {
  if (name.value.trim().length > 5) {
    test.value = true;
  } else {
    test.value = false;
  }
  s;
};
const show = () => {
  if (name.value.trim() !== "") {
    inview.value.push({ text: name.value.trim(), checked: false });
  }
  name.value = "";
  test.value = false;
};
const toggleCheck = (index) => {
  inview.value[index].checked = !inview.value[index].checked;
};
const deleteItem = (index) => {
  inview.value.splice(index, 1);
};
const clearall = () => {
  inview.value = [];
};
const checkedCount = computed(() => {
  return inview.value.filter((item) => item.checked).length;
});
const uncheckedCount = computed(() => {
  return inview.value.filter((item) => !item.checked).length;
});
</script>
<style scoped>
h1 {
  color: #42b983;
}
.checked {
  text-decoration: line-through;
  color: red;
  cursor: pointer;
}
li {
  cursor: pointer;
  margin-bottom: 4px;
}
#alrt {
  color: red;
  font-weight: bolder;
  text-transform: capitalize;
}
.draggable-fade-enter-active,
.draggable-fade-leave-active {
  transition: all 0.3s ease;
}
.draggable-fade-enter-from,
.draggable-fade-leave-to {
  opacity: 0;
  transform: translateY(10px);
}
ul {
  list-style: none;
  padding: 0;
}
li {
  padding: 5px 10px;
  background: #000000;
  margin-bottom: 5px;
  border-radius: 6px;
}
.fade-enter-active, .fade-leave-active {
  transition: all 0.4s ease;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
  transform: translateY(10px);
}
</style>
