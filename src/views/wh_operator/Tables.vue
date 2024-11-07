<script setup>
import { ref } from "vue";
// eslint-disable-next-line no-unused-vars
import AuthorsTable from "../components/AuthorsTable.vue";
// eslint-disable-next-line no-unused-vars
import ProjectsTable from "../components/ProjectsTable.vue";

const items = ref([
    { id: 1, name: 'Benang Poliéster', deskripsi: 'Benang berkualitas tinggi untuk menjahit', stok: 500, price: 'Rp 100.000' },
    { id: 2, name: 'Kain Katun', deskripsi: 'Kain katun untuk pembuatan pakaian', stok: 200, price: 'Rp 250.000' },
    { id: 3, name: 'Kain Spandex', deskripsi: 'Kain elastis untuk pakaian olahraga', stok: 150, price: 'Rp 300.000' },
    { id: 4, name: 'Kain Satin', deskripsi: 'Kain satin untuk busana formal', stok: 100, price: 'Rp 500.000' },
    { id: 5, name: 'Dye (Pewarna)', deskripsi: 'Pewarna tekstil untuk memberikan warna pada kain', stok: 300, price: 'Rp 50.000' },
    { id: 6, name: 'Bahan Pelapis', deskripsi: 'Bahan untuk pelapisan kain', stok: 250, price: 'Rp 200.000' },
    { id: 7, name: 'Furnitur Mesin Jahit', deskripsi: 'Peralatan untuk memproduksi pakaian', stok: 20, price: 'Rp 15.000.000' },
]);

const showForm = ref(false);
const selectedItem = ref(null);
const isEdit = ref(false);

function showAddForm() {
    selectedItem.value = { id: "", name: "", deskripsi: "", stok: "", price: "" };
    isEdit.value = false;
    showForm.value = true;
}

function editItem(item) {
    selectedItem.value = { ...item };
    isEdit.value = true;
    showForm.value = true;
}

function handleSubmit(item) {
    if (isEdit.value) {
        const index = items.value.findIndex((i) => i.id === item.id);
        if (index !== -1) {
            items.value.splice(index, 1, item);
        }
    } else {
        item.id = Date.now(); 
        items.value.push(item);
    }
    showForm.value = false;
    selectedItem.value = null;
    isEdit.value = false;
}

function cancelEditForm() {
    showForm.value = false;
    isEdit.value = false;
    selectedItem.value = null;
}

function deleteItem(id) {
    items.value = items.value.filter(item => item.id !== id);
}
</script>

<template>
    <div class="item-list">
        <div class="card">
            <div class="card-header d-flex justify-content-between align-items-center">
                <h2>Master Data</h2>
                <button @click="showAddForm" class="btn btn-primary">
                    <i class="bi bi-clipboard2-plus"></i> Tambah Item
                </button>
            </div>
            <div class="card-body">
                <table class="table table-bordered table-striped">
                    <thead>
                        <tr>
                            <th>Nama</th>
                            <th>Deskripsi</th>
                            <th>Stok</th>
                            <th>Harga</th>
                            <th>Aksi</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="item in items" :key="item.id">
                            <td>{{ item.name }}</td>
                            <td>{{ item.deskripsi }}</td>
                            <td>{{ item.stok }}</td>
                            <td>{{ item.price }}</td>
                            <td>
                                <button @click="editItem(item)" class="btn btn-warning btn-sm">
                                    <i class="bi bi-pencil-square"></i> Edit
                                </button>
                                <button @click="deleteItem(item.id)" class="btn btn-danger btn-sm">
                                    <i class="bi bi-trash3"></i> Delete
                                </button>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
        <Modal :visible="showForm" @close="cancelEditForm">
            <ItemForm
                :item="selectedItem"
                :isEdit="isEdit"
                @submit="handleSubmit"
                @cancel="cancelEditForm"
            />
        </Modal>
    </div>
</template>

<style scoped>
.item-list {
    width: 100%;
}
/* Tabel styling */
.table {
    width: 100%;
    margin-top: 20px;
}
</style>
