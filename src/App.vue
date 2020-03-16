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
</style>
