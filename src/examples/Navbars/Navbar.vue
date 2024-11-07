<script setup>
import { computed, ref } from "vue";
import { useStore } from "vuex";
import { useRoute, useRouter } from "vue-router";
import Breadcrumbs from "../Breadcrumbs.vue";

// eslint-disable-next-line no-unused-vars
const showMenu = ref(false);
const showRoleDropdown = ref(false);
const selectedRole = ref(null);  
const store = useStore();
const router = useRouter();
const isRTL = computed(() => store.state.isRTL);

const route = useRoute();

const currentRouteName = computed(() => route.name);
const currentDirectory = computed(() => {
  let dir = route.path.split("/")[1];
  return dir.charAt(0).toUpperCase() + dir.slice(1);
});

const minimizeSidebar = () => store.commit("sidebarMinimize");
const toggleConfigurator = () => store.commit("toggleConfigurator");

// Handle role selection
const handleRoleSelection = (role) => {
  selectedRole.value = role;
  showRoleDropdown.value = false;
  // Simpan role ke localStorage
  localStorage.setItem("userRole", role);
  // Arahkan ke dashboard sesuai dengan role
  if (role === "wh_operator") {
    router.push("/wh-operator");  
  } else if (role === "ph_operator") {
    router.push("/ph-operator");  
  }
};
</script>

<template>
  <nav class="navbar navbar-main navbar-expand-lg px-0 mx-4 shadow-none border-radius-xl"
    :class="isRTL ? 'top-0 position-sticky z-index-sticky' : ''" id="navbarBlur" data-scroll="true">
    <div class="px-3 py-1 container-fluid">
      <breadcrumbs :current-page="currentRouteName" :current-directory="currentDirectory" />
      <div class="mt-2 collapse navbar-collapse mt-sm-0 me-md-0 me-sm-4" :class="isRTL ? 'px-0' : 'me-sm-4'" id="navbar">
        <div class="pe-md-3 d-flex align-items-center" :class="isRTL ? 'me-md-auto' : 'ms-md-auto'">
          <div class="input-group">
            <span class="input-group-text text-body">
              <i class="fas fa-search" aria-hidden="true"></i>
            </span>
            <input type="text" class="form-control" :placeholder="isRTL ? 'أكتب هنا...' : 'Type here...'" />
          </div>
        </div>
        <ul class="navbar-nav justify-content-end">
          <!-- Role Dropdown -->
          <li class="nav-item dropdown d-flex align-items-center" :class="isRTL ? 'ps-2' : 'pe-2'">
            <a href="#" class="p-0 nav-link text-white" :class="[showRoleDropdown ? 'show' : '']"
               @click="showRoleDropdown = !showRoleDropdown">
              <i class="cursor-pointer fa fa-user"></i>
            </a>
            <ul class="px-2 py-3 dropdown-menu dropdown-menu-end me-sm-n4" :class="showRoleDropdown ? 'show' : ''">
              <li>
                <a class="dropdown-item" href="javascript:;" @click="handleRoleSelection('wh_operator')">
                  <span>WH Operator</span>
                </a>
              </li>
              <li>
                <a class="dropdown-item" href="javascript:;" @click="handleRoleSelection('ph_operator')">
                  <span>PH Operator</span>
                </a>
              </li>
            </ul>
          </li>
          <!-- Other Navbar Items -->
          <li class="nav-item d-xl-none ps-3 d-flex align-items-center">
            <a href="#" @click="minimizeSidebar" class="p-0 nav-link text-white" id="iconNavbarSidenav">
              <div class="sidenav-toggler-inner">
                <i class="sidenav-toggler-line bg-white"></i>
                <i class="sidenav-toggler-line bg-white"></i>
                <i class="sidenav-toggler-line bg-white"></i>
              </div>
            </a>
          </li>
          <li class="px-3 nav-item d-flex align-items-center">
            <a class="p-0 nav-link text-white" @click="toggleConfigurator">
              <i class="cursor-pointer fa fa-cog fixed-plugin-button-nav"></i>
            </a>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>
