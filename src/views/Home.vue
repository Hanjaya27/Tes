
<template>
  <div>

    <!-- Hero Section -->
    <section class="home" id="home">
      <div class="home-overlay">
        <div class="content">
          <h3>Mas Gondrong</h3>
          <p>Dari Mas Gondrong untuk perjalanan hebatmu</p>
          <a href="https://wa.me/6285353432343?text=Halo,%20saya%20tertarik%20untuk%20menyewa%20kendaraan%20dari%20Mas%20Gondrong." class="btn-pesan" target="_blank">Sewa Sekarang!</a>
        </div>
        <div class="image">
          <img src="@/assets/images/mobilbanner.png" alt="Mobil Banner" />
        </div>
      </div>
    </section>

    <!-- About Section -->
    <section class="about" id="about">
      <h1 class="heading"><span>Tentang </span> Kami</h1>
      <div class="row g-0">
        <div class="image">
          <img :src="require('@/assets/images/Banner(1).jpg')" alt="" class="img-fluid">
        </div>
        <div class="content">
          <h3>Sewa Kendaraan Lebih Mudah</h3>
          <p>
            Sewa Kendaraan Mas Gondrong adalah solusi sewa motor dan mobil terpercaya dengan proses mudah dan cepat.
            Temukan berbagai pilihan kendaraan sesuai kebutuhan Anda, pesan secara online, dan nikmati perjalanan tanpa ribet. 
            Aman, praktis, dan siap melayani di berbagai kota.
          </p>
          <a href="#" class="btn btn-dark text-decoration-none">Learn More</a>
        </div>
      </div>
    </section>

    <!-- Menu Section -->
    <section class="menu" id="menu">
      <h1 class="heading">Ketersediaan <span> Kendaraan</span></h1>
      <div class="d-flex">
        <select class="form-select me-2" v-model="kategoriDipilih">
          <option value="">Semua Kategori</option>
          <option value="mobil">Mobil</option>
          <option value="motor">Motor</option>
        </select>
      </div>
      <div class="box-container">
        <div class="container">
          <div class="row">
            <div class="col-md-4" v-for="(item, index) in kendaraanTersaring" :key="index">
              <div class="box">
                <img :src="require(`@/assets/images/${item.gambar}`)" :alt="item.nama" class="product-img" />
                <h3 class="product-title">{{ item.nama }}</h3>
                <div class="price">{{ item.harga }}</div>
                <button class="btn add-cart" @click.prevent="handleSewa(item.nama)">
                  Sewa Sekarang
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Review Section -->
    <section class="review" id="review">
      <h1 class="heading"><span>Testi</span>moni</h1>
      <div class="box-container">
        <div class="container">
          <div class="row">
            <div class="col-md-4" v-for="(review, i) in testimonials" :key="i">
              <div class="box">
                <p>{{ review.text }}</p>
                <img :src="require('@/assets/images/logo.jpg')" alt="" class="user" />
                <h3>{{ review.nama }}</h3>
                <div class="stars">
                  <i class="fas fa-star" v-for="s in review.rating" :key="s"></i>
                </div>
              </div>
            </div>
          </div>
        </div>  
      </div>
    </section>

    <!-- Contact Section -->
    <section class="contact" id="contact">
      <h1 class="heading"><span>Hubungi </span> Kami</h1>
      <div class="row">
        <div id="map" class="map pull-left"></div>
        <form name="contact" method="POST" action="https://formspree.io/f/xayzavgb">
          <h3> Hubungi kami!</h3>
          <div class="inputBox">
            <input type="email" name="email" placeholder="Email Address">
          </div>
          <div class="inputBox">
            <textarea name="message" placeholder="Enter your message..."></textarea>
          </div>
          <button type="submit" class="btn">Hubungi sekarang</button>
        </form>
      </div>
    </section>

  </div>
</template>

<script>
import { onMounted, ref, computed } from 'vue'
import { useRouter } from 'vue-router'

export default {
  name: 'HomePage',
  setup() {
    const router = useRouter()

    const kendaraan = ref([
      { nama: 'Honda Beat', gambar: 'Beat.jpg', harga: 'Rp.100.000/hari', kategori: 'motor' },
      { nama: 'Honda Scoopy', gambar: 'Scoopy.jpg', harga: 'Rp.125.000/hari', kategori: 'motor' },
      { nama: 'Honda Vario', gambar: 'vario.jpg', harga: 'Rp.150.000/hari', kategori: 'motor' },
      { nama: 'Toyota Avanza', gambar: 'Pajero.jpg', harga: 'Rp.400.000/hari', kategori: 'mobil' },
      { nama: 'Brio', gambar: 'Brio.jpeg', harga: 'Rp.375.000/hari', kategori: 'mobil' },
      { nama: 'Daihatsu Xenia', gambar: 'Innova.jpg', harga: 'Rp.500.000/hari', kategori: 'mobil' }
    ])

    const kategoriDipilih = ref('')

    const kendaraanTersaring = computed(() => {
      if (!kategoriDipilih.value) return kendaraan.value
      return kendaraan.value.filter(k => k.kategori === kategoriDipilih.value)
    })

    const testimonials = ref([
      { nama: 'Danang', text: 'Pelayanannya cepat dan motornya bersih! Saya sewa Beat 3 hari dan semuanya lancar. Mas Gondrong juga ramah banget!', rating: 5 },
      { nama: 'Ubay', text: 'Mobil Avanza yang saya sewa nyaman dipakai untuk perjalanan keluarga. Harganya juga bersahabat. Recommended!', rating: 5 },
      { nama: 'Brodin', text: 'Pertama kali ke Jogja dan bingung cari kendaraan. Untung ketemu Sewa Kendaraan Mas Gondrong. Prosesnya gampang, motor langsung diantar ke hotel.', rating: 5 }
    ])

    const handleSewa = (namaKendaraan) => {
      const isLoggedIn = localStorage.getItem('user')
      if (!isLoggedIn) {
        alert('Silakan login terlebih dahulu untuk melakukan pemesanan.')
        router.push('/login')
        return
      }
      router.push({ name: 'Pemesanan', params: { kendaraan: namaKendaraan } })
    }

    onMounted(() => {
      const L = window.L
      const map = L.map('map').setView([-7.7599, 110.4090], 16)
      L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        attribution: '&copy; OpenStreetMap contributors'
      }).addTo(map)

      L.marker([-7.7599, 110.4090]).addTo(map)
        .bindPopup('Universitas Amikom Yogyakarta')
        .openPopup()
    })

    return {
      kendaraan,
      kategoriDipilih,
      kendaraanTersaring,
      testimonials,
      handleSewa
    }
  }
}
</script>

<style scoped>

</style>
