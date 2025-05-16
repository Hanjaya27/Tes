<template>
  <div class="container pemesanan-wrapper">
    <div class="card shadow">
      <div class="card-body">
        <!-- Info Kendaraan -->
        <div class="text-center mb-3">
          <img src="@/assets/images/Scoopy.jpg" alt="Honda Scoopy" class="img-fluid kendaraan-img" />
          <h5 class="mt-3">Honda Scoopy</h5>
          <p class="text-muted">Motor matic irit dan nyaman digunakan, cocok untuk harian.</p>
        </div>

        <!-- Form -->
        <form @submit.prevent="pesanKendaraan">
          <div class="mb-3">
            <label for="tgl_mulai" class="form-label">Tanggal Mulai</label>
            <input type="date" v-model="tglMulai" class="form-control" id="tgl_mulai" required />
          </div>

          <div class="mb-3">
            <label for="tgl_selesai" class="form-label">Tanggal Selesai</label>
            <input type="date" v-model="tglSelesai" class="form-control" id="tgl_selesai" required />
          </div>

          <div class="text-center mb-3">
            <div class="total-harga">Total Harga: Rp 125.000</div>
          </div>

          <router-link to="/pembayaran" class="btn btn-green w-100">Pesan Sekarang</router-link>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PemesananPage',
  data() {
    return {
      tglMulai: '',
      tglSelesai: ''
    };
  },
  methods: {
    pesanKendaraan() {
      // Logika penyimpanan atau validasi bisa ditambahkan di sini
      console.log(`Tanggal mulai: ${this.tglMulai}, Tanggal selesai: ${this.tglSelesai}`);
    }
  }
};
</script>

<style scoped>
.pemesanan-wrapper {
  max-width: 500px;
  margin: 80px auto;
}
.total-harga {
  font-weight: bold;
  font-size: 1.2rem;
}
.kendaraan-img {
  width: 100%;
  max-height: 250px;
  object-fit: cover;
}
</style>
