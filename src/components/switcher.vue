<template>
  <div>
    <label>
      <input type="radio" v-model="activeComponent" :value="DragComponent"> Drag
    </label>
    <label>
      <input type="radio" v-model="activeComponent" :value="ListComponent"> List
    </label>
    <label>
      <input type="radio" v-model="activeComponent" :value="NumbComponent"> Numbers
    </label>

    <Transition name="fade" mode="out-in">
      <component :is="activeComponent"></component>
    </Transition>
  </div>
</template>

<script>
import { shallowRef } from 'vue';
import DragComponent from './drag.vue';
import ListComponent from './list.vue';
import NumbComponent from './numb.vue';

export default {
  setup() {
    const activeComponent = shallowRef(DragComponent);
    return { activeComponent, DragComponent, ListComponent, NumbComponent };
  },
};
</script>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>