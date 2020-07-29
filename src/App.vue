<template>
  <div id="app">
    <div id="nav"></div>
    <transition name="router-anim" mode="out-in">
      <router-view />
    </transition>
  </div>
</template>
<script></script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.router-anim-enter-active {
  animation: coming 0.8s;
  opacity: 0;
}
.router-anim-leave-active {
  animation: going 0.8s;
}

@keyframes going {
  from {
    transform: translateX(0);
  }
  to {
    transform: translateX(100%);
    opacity: 0;
  }
}
@keyframes coming {
  from {
    transform: translateX(-100%);
  }
  to {
    transform: translateX(0);
    opacity: 1;
  }
}
</style>
