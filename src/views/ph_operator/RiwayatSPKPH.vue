<template>
  <div class="history-list">
    <h2>Riwayat Pengajuan SPK</h2>
    <button @click="print" class="btn btn-primary mb-4">
      <i class="bi bi-printer"></i> Cetak Laporan
    </button>
    <div class="table-responsive" id="print-section">
      <table class="table table-striped table-bordered">
        <thead class="thead-dark">
          <tr>
            <th>ID</th>
            <th>Nama Karyawan</th>
            <th>Tanggal Pengajuan</th>
            <th>SPK</th>
            <th>Status</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="history in histories" :key="history.id">
            <td>{{ history.id }}</td>
            <td>{{ history.namaKaryawan }}</td>
            <td>{{ history.tanggalPengajuan }}</td>
            <td>
              <a :href="history.spkLink" target="_blank" class="btn btn-link">Unduh SPK</a>
            </td>
            <td :class="['status', history.status.toLowerCase()]">
              {{ history.status }}
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: "HistoryList",
  data() {
    return {
      histories: [
        {
          id: 1,
          namaKaryawan: "Doni Monardo",
          tanggalPengajuan: "2024-01-01",
          spkLink: "https://drive.google.com/file/d/1eE_L0n1G8gc66qSkm6UtCsBocnFc78_j/view?usp=sharing",
          status: "done",
        },
        {
          id: 2,
          namaKaryawan: "Doni Monardo",
          tanggalPengajuan: "2024-01-02",
          spkLink: "https://drive.google.com/file/d/1eE_L0n1G8gc66qSkm6UtCsBocnFc78_j/view?usp=sharing",
          status: "done",
        },
        {
          id: 3,
          namaKaryawan: "Doni Monardo",
          tanggalPengajuan: "2024-01-03",
          spkLink: "https://drive.google.com/file/d/1eE_L0n1G8gc66qSkm6UtCsBocnFc78_j/view?usp=sharing",
          status: "done",
        },
        {
          id: 4,
          namaKaryawan: "Doni Monardo",
          tanggalPengajuan: "2024-01-04",
          spkLink: "https://drive.google.com/file/d/1eE_L0n1G8gc66qSkm6UtCsBocnFc78_j/view?usp=sharing",
          status: "done",
        },
      ],
    };
  },
  methods: {
    print() {
      window.print();
    },
  },
};
</script>

<style scoped>
.history-list {
  width: 100%;
  padding: 16px;
  background-color: #fff;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  margin: 8px 0;
}

h2 {
  margin-bottom: 20px;
  color: #080808;
  text-align: center;
  font-size: 24px;
  font-weight: bold;
}

/* Tabel Styling */
.table {
  width: 100%;
  border-collapse: collapse;
}

.table-striped tbody tr:nth-of-type(odd) {
  background-color: #f9f9f9;
}

.table th,
.table td {
  padding: 12px 15px;
  text-align: left;
}

.table th {
  background-color: #343a40;
  color: white;
  text-transform: uppercase;
}

.table-bordered th,
.table-bordered td {
  border: 1px solid #dee2e6;
}

.table a.btn-link {
  text-decoration: none;
  color: #007bff;
}

.table .status {
  text-transform: capitalize;
  font-weight: bold;
  color: #fff;
  padding: 5px 10px;
  border-radius: 4px;
  text-align: center;
}

.table .status.done {
  background-color: #28a745;
}

.table .status.pending {
  background-color: #ffc107;
}

.table .status.rejected {
  background-color: #dc3545;
}

/* CSS untuk tampilan print */
@media print {
  body * {
    visibility: hidden;
  }
  #print-section,
  #print-section * {
    visibility: visible;
  }
  #print-section {
    position: absolute;
    left: 0;
    top: 0;
  }
}
</style>
