<template>
  <main>
    <!-- Hero Section -->
    <section class="home" id="home">
      <div class="home-overlay">
        <div class="content">
          <h1>Mas Gondrong</h1>
          <p>Dari Mas Gondrong untuk perjalanan hebatmu</p>
          <button class="btn-pesan" @click.prevent="handleSewa()">Sewa Sekarang!</button>
        </div>
        <div class="image">
          <img src="@/assets/images/mobillbanner.png" alt="Banner perusahaan" class="img-fluid" width="600" height="400">
        </div>
      </div>
    </section>

    <!-- About Section -->
    <section class="about" id="about">
      <h1 class="heading"><span>Tentang </span> Kami</h1>
      <div class="row g-0">
        <div class="image">
          <img :src="require('@/assets/images/Banner(1).jpg')" alt="Banner perusahaan" class="img-fluid" width="600" height="400">
        </div>
        <div class="content">
          <h2>Sewa Kendaraan Lebih Mudah</h2>
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
        <label for="kategori">Pilih Kategori:</label>
        <select id="kategori" class="form-select me-2" v-model="kategoriDipilih">
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
                <img 
                  :src="require(`@/assets/images/${item.gambar}`)"
                  :alt="`Gambar kendaraan ${item.nama}`"
                  class="product-img"
                  width="300"
                  height="200"
                />
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
                <img :src="require('@/assets/images/logo.jpg')" :alt="`Foto pelanggan ${review.nama}`" class="user" width="100" height="100" />
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
        <div class="col-md-6">
          <iframe
            title="Lokasi Universitas Amikom Yogyakarta"
            src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3952.888244166353!2d110.4067900147768!3d-7.759886594417775!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x2e7a5919b92b0129%3A0xe7d9a243203d2975!2sUniversitas%20Amikom%20Yogyakarta!5e0!3m2!1sid!2sid!4v1683458015786!5m2!1sid!2sid"
            width="100%"
            height="300"
            style="border:0; border-radius: 12px;"
            allowfullscreen=""
            loading="lazy"
            referrerpolicy="no-referrer-when-downgrade"
          ></iframe>
          <div class="mt-2">
            <a href="https://goo.gl/maps/HScGnEY4CN6UizdXA" target="_blank" rel="noopener" class="text-primary">Lihat peta lebih besar</a>
          </div>
        </div>
        <div class="col-md-6">
          <form name="contact" method="POST" action="https://formspree.io/f/xayzavgb">
            <h3> Hubungi kami!</h3>
            <a href="https://wa.me/6285353432343?text=Halo,%20saya%20tertarik%20untuk%20menyewa%20kendaraan%20dari%20Mas%20Gondrong." class="btn-pesan" target="_blank">Hubungi Kami!</a>
            <div class="inputBox">
              <label for="email">Alamat Email</label>
              <input type="email" id="email" name="email" placeholder="Email Address">
            </div>
            <div class="inputBox">
              <label for="message">Pesan</label>
              <textarea id="message" name="message" placeholder="Enter your message..."></textarea>
            </div>
            <button type="submit" class="btn">Hubungi sekarang</button>
          </form>
        </div>
      </div>
    </section>

    <!-- WhatsApp Floating Button -->
    <a
      href="https://wa.me/6285353432343?text=Halo,%20saya%20tertarik%20dengan%20layanan%20sewa%20kendaraan%20Mas%20Gondrong."
      class="whatsapp-float"
      target="_blank"
      rel="noopener"
      aria-label="Hubungi Mas Gondrong melalui WhatsApp"
    >
      <img src="https://img.icons8.com/color/48/000000/whatsapp--v1.png" alt="WhatsApp" width="48" height="48" />
    </a>
  </main>
</template>

<script>
import { ref, computed } from 'vue'
import { useRouter } from 'vue-router'

export default {
  name: 'HomePage',
  setup() {
    const router = useRouter()

    const kendaraan = ref([
      { nama: 'Honda Beat', gambar: 'Beat.jpg', harga: 'Rp.100.000/hari', kategori: 'motor' },
      { nama: 'Honda Scoopy', gambar: 'Scoopy.jpg', harga: 'Rp.125.000/hari', kategori: 'motor' },
      { nama: 'Honda Vario', gambar: 'vario.jpg', harga: 'Rp.150.000/hari', kategori: 'motor' },
      { nama: 'Mitsubishi Pajero', gambar: 'Pajero.jpg', harga: 'Rp.800.000/hari', kategori: 'mobil' },
      { nama: 'Brio', gambar: 'Brio.jpeg', harga: 'Rp.375.000/hari', kategori: 'mobil' },
      { nama: 'Toyota Zenix', gambar: 'Innova.jpg', harga: 'Rp.500.000/hari', kategori: 'mobil' }
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
