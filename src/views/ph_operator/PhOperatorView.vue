<template>
  <div>
    <h3>PH Operator Dashboard</h3>
    <router-view></router-view> <!-- Tempat untuk memuat child routes -->
    
    <!-- Daftar fitur khusus untuk PH Operator -->
    <ul>
      <li>
        <router-link to="/ph-operator/master-data">Master Data</router-link>
      </li>
      <div v-if="currentComponent === 'master-data'">
      <div class="component-container">
        <MasterData />
      </div>
    </div>
      <li>
        <router-link to="/ph-operator/pengajuan-spk">Pengajuan SPK</router-link>
      </li>
      <div v-if="currentComponent === 'Pengajuan-spk'">
      <div class="component-container">
        <PengajuanSPK />
      </div>
    </div>
      <li>
        <router-link to="/ph-operator/riwayat-spk">Riwayat SPK</router-link>
      </li>
      <div v-if="currentComponent === 'riwayat-spk'">
      <div class="component-container">
        <RiwayatSPKPH />
      </div>
    </div>
    </ul>
  </div>
</template>

<script setup>
import MasterData from "./MasterData.vue";
import PengajuanSPK from "./PengajuanSPK.vue";
import RiwayatSPKPH from "./RiwayatSPKPH.vue";
</script>

<style scoped>
/* Style spesifik untuk PH Operator Dashboard */
h1 {
  color: #f44336;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  margin: 10px 0;
}
</style>

