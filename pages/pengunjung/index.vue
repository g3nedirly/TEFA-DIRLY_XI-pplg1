<template>
    <div class="container-fluid">
      <div class="row">
        <div class="col-lg-12">
          <h2 class="text-center my-4">RIWAYAT KUNJUNGAN</h2>
          <div class="my-3">
            <input type="search" class="form-control form-control-lg rounded-5" placeholder="Filter...">
          </div>
          <div class="my-3 text-muted">Menampilkan 1 dari 1</div>
          <table class="table table-bordered">
            <thead>
              <tr>
                <td>#</td>
                <td>NAMA</td>
                <td>KEANGOTAAN</td>
                <td>WAKTU</td>
                <td>KEPERLUAN</td>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(visitor,i) in visitors" :key="i">
              <td>{{ i+1 }}.</td>
              <td>{{ visitor.nama }}</td>
              <td>{{ visitor.keanggotaan?.nama }}</td>
              <td>{{ visitor.tanggal }}, {{ visitor.waktu }}</td>
              <td>{{ visitor.keperluan?.nama }}</td>
            </tr>
            </tbody>
          </table>
          <nuxt-link to="/">
            <button type="submit" class="form-kirim btn btn-secondary btn-lg rounded-5 px-5">kembali</button>
          </nuxt-link>
          
        </div>
      </div>
    </div>
</template>
  
  <script setup>
  const supabase = useSupabaseClient()
  
  const visitors = ref ([])
  
  const getPengunjung = async () => {
    const { data, error } = await supabase.from('pengunjung').select(`*, keanggotaan(*), keperluan(*)`)
    if(data) visitors.value = data
  }
  
  onMounted(() => {
    getPengunjung()
  })
  </script>
  <style scoped>
.btn{
  background-color: rgb(172, 169, 175);
}
.form-control{
  background-color: rgb(172, 169, 175);
}
</style>                                                                                                                                                                                                                                                                                                                                                                                                 