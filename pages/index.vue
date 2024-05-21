<template>
    <div class="container-fluid">
      <div class="row my-5 justify-content-around">
        <div class="col-lg-5">
          <nuxt-link to="/pengunjung/tambah">
            <div class="card bg-pengunjung rounded-5">
              <div class="card-body">
                <h2 style="font-family: ">Pengunjung</h2>
              </div>
            </div>
          </nuxt-link>
        </div>
        <div class="col-lg-5"> 
          <nuxt-link to="/buku">
            <div class="card bg-buku rounded-5">
              <div class="card-body">
                <h2 style="font-family: ">Cari Buku</h2>
              </div>
            </div>
          </nuxt-link>
        </div>
        </div>
  
        <h2 class="mt-5" style="margin-left: 150px;">STATISTIK</h2>
        <div class="row my-5 justify-content-around">
          <div class="col-lg-5">
            
              <div class="card bg-spengunjung rounded-5">
              <div class="card-body">
                <div class="row">
                  <div class=" form-pengunjung col p-5"></div>
                  <div class="form-pengunjung col mt-5 p-5"><h2 style="font-size: 70px; margin-right: 80px "><span class="no">{{ jml_pengunjung }}</span>Pengunjung</h2></div>
                </div>
              </div>
            </div>
            
          </div>
  
        <div class="col-lg-5">
       
            <div class="card bg-sbuku rounded-5">
              <div class="card-body">
                <div class="row">
                  <div class="col p-5"></div>
                  <div class="col mt-5 p-5"><h2 style="font-size: 70px; margin-right: 200px"><span class="no">{{ jml_buku }}</span>Buku</h2></div>
                </div>
              </div>
            </div>
          </div>
        </div>
    </div>
      <div>
        <div class="line">
          <Statistik></Statistik>
        </div>
      </div>
  </template>

  <script setup>
  const supabase = useSupabaseClient()
  const jml_pengunjung = ref(0)
  const jml_buku = ref(0)

  async function getjml_pengunjung() {
    const{error, data, count } = await supabase
    .from("pengunjung")
    .select('*', {count: 'exact' })
    if (count) jml_pengunjung.value = count
  }

  async function getjml_buku() {
    const{error, data, count } = await supabase
    .from("Buku")
    .select('*', {count: 'exact' })
    if (count) jml_buku.value = count
  }

onMounted(() => {
  getjml_pengunjung()
  getjml_buku( )
})

</script>
  
  
  <style scoped>
  .card {
    height: 250px;
    box-shadow: 1px 1px 10px #424242;
  }
  .card.bg-pengunjung { 
    background-image: url('../assets/img/bg kunjungan.jpeg');
    background-repeat: no-repeat;
    background-position: center center;
    background-size: cover;
    opacity: 60%;
  }
  .card.bg-buku { 
    background-image: url('../assets/img/bg cari-buku.jpg');
    background-repeat: no-repeat;
    background-position: center center;
    background-size: cover;
    opacity: 60%;
  }
  .card.bg-spengunjung { 
    background-color: #ECEE7F;
    background-repeat: no-repeat;
    background-position: center center;
    background-size: cover;
    opacity: 60%;
  }
  .card.bg-sbuku { 
    background-color: #A8FFEF;
    background-repeat: no-repeat;
    background-position: center center;
    background-size: cover;
    opacity: 60%;
  }

  </style>