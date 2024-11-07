<script setup>
import { useRoute } from "vue-router";
import SidenavItem from "./SidenavItem.vue";
import SidenavCard from "./SidenavCard.vue";

// Mendapatkan path untuk menentukan halaman yang aktif
const getRoute = () => {
  const route = useRoute();
  return route.name; // Menggunakan route.name untuk mencocokkan dengan nama route
};


// Menambahkan props role yang akan digunakan untuk menentukan akses ke menu sidebar
defineProps({
  role: {
    type: String,
    required: true
  }
});
</script>

<template>
  <div class="collapse navbar-collapse w-auto h-auto h-100" id="sidenav-collapse-main">
    <ul class="navbar-nav">
      <!-- Dashboard (Tampil untuk semua role) -->
      <li class="nav-item">
        <sidenav-item
          to="/dashboard-default"
          :class="getRoute() === 'dashboard-default' ? 'active' : ''"
          navText="Dashboard"
        >
          <template v-slot:icon>
            <i class="ni ni-tv-2 text-primary text-sm opacity-10"></i>
          </template>
        </sidenav-item>
      </li>

      <!-- Menu untuk WH Operator -->
      <template v-if="role === 'wh_operator'">
        <li class="nav-item">
          <sidenav-item
            to="/tables"
            :class="getRoute() === 'wh_operator_tables' ? 'active' : ''"
            navText="Master Data"
          >
            <template v-slot:icon>
              <i class="ni ni-calendar-grid-58 text-warning text-sm opacity-10"></i>
            </template>
          </sidenav-item>
        </li>

        <li class="nav-item">
          <sidenav-item
            to="/spk-masuk"
            :class="getRoute() === 'wh_operator_spk-masuk' ? 'active' : ''"
            navText="SPK Masuk"
          >
            <template v-slot:icon>
              <i class="ni ni-credit-card text-success text-sm opacity-10"></i>
            </template>
          </sidenav-item>
        </li>

        <li class="nav-item">
          <sidenav-item
            to="/riwayat-spk" 
            :class="getRoute() === 'wh_operator_riwayat-spk' ? 'active' : ''"
            navText="Riwayat SPK"
          >
            <template v-slot:icon>
              <i class="ni ni-app text-info text-sm opacity-10"></i>
            </template>
          </sidenav-item>
        </li>

        <li class="nav-item">
          <sidenav-item
            to="/profile" 
            :class="getRoute() === 'wh_operator_profile' ? 'active' : ''"
            navText="Profile"
          >
            <template v-slot:icon>
              <i class="ni ni-app text-info text-sm opacity-10"></i>
            </template>
          </sidenav-item>
        </li>
      </template>

      <!-- Menu untuk PH Operator -->
      <template v-if="role === 'ph_operator'">
        <li class="nav-item">
          <sidenav-item
            to="/master-data"
            :class="getRoute() === 'ph_operator_master-data' ? 'active' : ''"
            navText="Master Data"
          >
            <template v-slot:icon>
              <i class="ni ni-calendar-grid-58 text-warning text-sm opacity-10"></i>
            </template>
          </sidenav-item>
        </li>

        <li class="nav-item">
          <sidenav-item
            to="/pengajuan-spk"
            :class="getRoute() === 'ph_operator_pengajuan-spk' ? 'active' : ''"
            navText="Pengajuan SPK"
          >
            <template v-slot:icon>
              <i class="ni ni-calendar-grid-58 text-warning text-sm opacity-10"></i>
            </template>
          </sidenav-item>
        </li>

        <li class="nav-item">
          <sidenav-item
            to="/riwayat-spk"
            :class="getRoute() === 'ph_operator_riwayat-spk' ? 'active' : ''"
            navText="Riwayat SPK"
          >
            <template v-slot:icon>
              <i class="ni ni-calendar-grid-58 text-warning text-sm opacity-10"></i>
            </template>
          </sidenav-item>
        </li>
      </template>

      <!-- Menu Akun (Tampil untuk semua role) -->
      <li class="mt-3 nav-item">
        <h6 class="text-xs ps-4 text-uppercase font-weight-bolder opacity-6 ms-2">
          ACCOUNT PAGES
        </h6>
      </li>

      <li class="nav-item">
        <sidenav-item
          to="/signin"
          :class="getRoute() === 'signin' ? 'active' : ''"
          navText="Sign In"
        >
          <template v-slot:icon>
            <i class="ni ni-single-copy-04 text-danger text-sm opacity-10"></i>
          </template>
        </sidenav-item>
      </li>

      <li class="nav-item">
        <sidenav-item
          to="/signup"
          :class="getRoute() === 'signup' ? 'active' : ''"
          navText="Sign Up"
        >
          <template v-slot:icon>
            <i class="ni ni-collection text-info text-sm opacity-10"></i>
          </template>
        </sidenav-item>
      </li>
    </ul>
  </div>

  <div class="pt-3 mx-3 mt-3 sidenav-footer">
    <sidenav-card
      :card="{
        title: 'Need Help?',
        description: 'Please check our docs',
        links: [
          {
            label: 'Documentation',
            route:
              'https://www.creative-tim.com/learning-lab/vue/overview/argon-dashboard/',
            color: 'dark',
          },
          {
            label: 'Buy now',
            route:
              'https://www.creative-tim.com/product/vue-argon-dashboard-pro?ref=vadp',
            color: 'success',
          },
        ],
      }"
    />
  </div>
</template>
