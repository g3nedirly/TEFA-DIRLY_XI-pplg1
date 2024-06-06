<template>
    <div class="container-fluid">
      <div class="row">
        <div class="col-lg-12">
          <h2 class="text-center my-4">RIWAYAT KUNJUNGAN</h2>
          <div class="my-3">
            <form  @submit.prevent="getBuku">
                        <input v-model="keyword" type="search" class="form-control rounded-5" placeholder="Filter...">
                    </form>
          </div>
          <div class="my-3 text-muted">menampilkan {{ visitors?.length }} dari {{ totalBuku }}</div>
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
  const keyword = ref('')
  const visitors = ref ([])
  const totalBuku = ref(0);
  
  const getPengunjung = async () => {
    const { data, error } = await supabase.from('pengunjung').select(`*, keanggotaan(*), keperluan(*)`)
    if(data) visitors.value = data
  }
  const getBuku = async () => {
    const {data,error} = await supabase.from('pengunjung').select(`*, keanggotaan(*), keperluan(*)`)
        .ilike('nama', `%${keyword.value}%`)
    if(data) visitors.value = data
}
const getTotalBuku = async () => {
  const { count, error } = await supabase.from('pengunjung').select(`*, keanggotaan(*), keperluan(*)`, { count: "exact", head: true });
  if (error) throw error
  if (count) totalBuku.value = count;
};


  onMounted(() => {
    getPengunjung()
    getBuku()
    getTotalBuku()
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