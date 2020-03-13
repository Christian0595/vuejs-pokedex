<template>
  <section class="hero">
    <div class="hero-inner">
      <div id="app">
        <transition name="component-fade" mode="out-in">
          <router-view></router-view>
        </transition>
      </div>
    </div>
  </section>
</template>

<script>

export default {
  name: 'App'
}
</script>

<style>
.component-fade-leave-active {
  transition: opacity 0.5s ease;
}
.component-fade-enter, .component-fade-leave-to
/* .component-fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
