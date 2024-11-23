<template>
  <TheNavigation/>
  <div class="container">
    <!-- Sidebar -->
    <router-view v-slot="{Component}" class="view left-sidebar" name="LeftSidebar">
      SIdebar
      <transition name="fade" mode="out-in">
        <Component :is="Component" :key="$route.path"></Component>
      </transition>
    </router-view>

    <!-- Main -->
    <router-view v-slot="{Component}" class="main-view">
      Main
      <transition name="fade" mode="out-in">
        <Component :is="Component" :key="$route.path"></Component>
      </transition>
    </router-view>
  </div>
</template>

<script>
import TheNavigation from './components/TheNavigation.vue';
export default {
  components: {TheNavigation}
}
</script>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 1s;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.container {
  display: flex;
}

.left-sidebar {
  width: 20%;
}

.main-view {
  width: 100%;
}
</style>
