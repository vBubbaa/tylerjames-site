<template>
  <!-- non-mobile view -->
  <nav class="p-4 flex flex-auto" v-if="!isMobile">
    <div class="flex-start flex-1">
      <img src="../assets/logo.png" alt="Logo" width="50" height="50" />
    </div>
    <div class="flex-end items-center flex">
      <a class="px-2">item</a>
      <a class="px-2">item</a>
      <a class="px-2">item</a>
    </div>
  </nav>
  <!-- mobile view -->
  <nav class="flex flex-auto flex-col" v-else>
    <div
      class="p-4 flex-row flex"
      :class="{ openDrawerStyle: drawerOpen, headerOpenDrawer: drawerOpen }"
    >
      <div class="flex-start flex-1">
        <img src="../assets/logo.png" alt="Logo" width="50" height="50" />
      </div>
      <div class="flex-end items-center flex">
        <svg-icon
          :fa-icon="faBars"
          :size="50"
          class="nav-bars"
          :class="{ 'nav-bars-drawerOpen': drawerOpen }"
          @click="handleDrawer"
        ></svg-icon>
      </div>
    </div>
    <Transition name="drawer-slide-down">
      <div
        v-if="drawerOpen"
        class="flex-col"
        :class="{ openDrawerStyle: drawerOpen }"
      >
        <div class="flex justify-center py-4"><a>item</a></div>
        <div class="flex justify-center py-4"><a>item</a></div>
        <div class="flex justify-center py-4"><a>item</a></div>
      </div>
    </Transition>
  </nav>
</template>

<script>
import { onMounted, ref } from "vue";
import SvgIcon from "vue3-icon";
import { faBars } from "@fortawesome/free-solid-svg-icons";

export default {
  components: {
    SvgIcon,
  },
  name: "Navbar",
  setup() {
    // isMobile controller
    let isMobile = ref(false);
    // value we use to track if the mobile drawer is open
    let drawerOpen = ref(false);

    // handle resizing of page (using tailwind mobile breakpoint @640px)
    const handleResize = () => {
      isMobile.value = window.innerWidth < 640;
    };

    // drawer open handler -> change drawerOpen value
    const handleDrawer = () => {
      drawerOpen.value = !drawerOpen.value;
    };

    // on mounted, check the handleResize to set the inital ismobile value, then add resize event listener to continuously set isMobile value
    onMounted(() => {
      handleResize();
      window.addEventListener("resize", handleResize);
    });

    return {
      isMobile,
      faBars,
      drawerOpen,
      handleDrawer,
    };
  },
};
</script>

<style>
.nav-bars:hover {
  color: #f87060;
}

.nav-bars:hover * {
  color: #f87060;
}

.openDrawerStyle {
  transition: background-color 0.3s ease;
  background-color: white;
}

.openDrawerStyle a {
  color: #f87060;
  font-size: 1.5rem;
}

.headerOpenDrawer {
  border-bottom: 1px solid #102542;
}

.nav-bars-drawerOpen * {
  color: #102542;
}

/* drawer transition animations */
.drawer-slide-down-enter-active {
  transition: all 0.3s ease-out;
}

.drawer-slide-down-leave-active {
  transition: all 0.3s cubic-bezier(1, 0.5, 0.8, 1);
}

.drawer-slide-down-enter-from,
.drawer-slide-down-leave-to {
  transform: translateY(-20px);
  opacity: 0;
}
</style>