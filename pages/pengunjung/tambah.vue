<template>
  <div class="container-fluid">
      <div class="row">
          <div class="col-lg 12">
              <h2 class="text-center my-4">ISI BUKU KUNJUNGAN</h2>
              <form @submit.prevent="kirimData">
                  <div class="mb-3">
                      <input v-model="form.nama" type="text" class="form-nama form-control form control-lg rounded-5" placeholder="NAMA...">
                  </div>
                  <div class="mb-3">
                      <select v-model="form.keanggotaan" class="form-keanggotaan keanggotaan form-control form-control-lg form-select rounded-5" >
                        <option value="">Keanggotaan</option>
                          <option v-for="(member,i) in members" :key="i" :value="member.id">{{ member.nama }}</option>
                      </select>
                  </div>
                  <div v-if="form.keanggotaan == 1" class="mb-3">
                      <div class="row">
                          <div class="col-md-4">
                              <select v-model="form.tingkat" class="form-tingkat form-control form-control-lg form-select rounded-5 mb-2">
                                  <option value="">TINGKAT</option>
                                  <option value="X">X</option>
                                  <option value="XI">XI</option>
                                  <option value="XII">XII</option>
                              </select>
                          </div>
                          <div class="col-md-4">
                              <select v-model="form.jurusan" class="form-jurusan form-control form-control-lg form-select rounded-5 mb-2">
                                  <option value="">JURUSAN</option>
                                  <option value="PPLG">PPLG</option>
                                  <option value="TJKT">TJKT</option>
                                  <option value="TSM">TSM</option>
                                  <option value="DKV">DKV</option>
                                  <option value="TOI">TOI</option>
                              </select>
                          </div>
                          <div class="col-md-4">
                              <select v-model="form.kelas" class="form-kelas form-control form-control-lg form-select rounded-5 mb-2">
                                  <option value="">KELAS</option>
                                  <option value="1">1</option>
                                  <option value="2">2</option>
                                  <option value="3">3</option>
                                  <option value="4">4</option>
                              </select>
                          </div>
                      </div>
                  </div>
                  <div class="mb-3">
                      <select v-model="form.keperluan" class="form-keperluan form-control form-control-lg form-select rounded-5">
                          <option value="">KEPERLUAN</option>
                          <option v-for="(item,i) in objectives" :key="i" :value="item.id">{{ item.nama }}</option>
                      </select>
                  </div>

                    <button type="submit" class="form-kirim btn btn-secondary btn-lg rounded-5 px-5">KIRIM</button>

                 
              </form>
          </div>
      </div>
  </div>
</template>

<script setup>

const supabase = useSupabaseClient()

const members = ref ([])
const objectives = ref ([])

const form = ref ({
    nama: "",
    keanggotaan: "",
    tingkat: "",
    jurusan: "",
    kelas: "",
    keperluan: "",
})

const kirimData = async () => {
    const { error } = await supabase.from('pengunjung').insert([form.value])
    if(error) throw error
    else navigateTo('/pengunjung')
    
}
const getkeanggotaan = async () => {
    const { data, error } = await supabase.from('keanggotaan').select('*')
    if(data) members.value = data
}
const getkeperluan= async () => {
    const { data, error } = await supabase.from('keperluan').select('*')
    if(data) objectives.value = data
}

onMounted(() => {
    getkeanggotaan()
    getkeperluan()
})

</script>

<style scoped>
    .form-nama{
        background-color: rgb(172, 169, 175);
    }
    .form-keanggotaan{
    background-color: rgb(172, 169, 175);
    }
    .form-tingkat{
    background-color: rgb(172, 169, 175);
    }
    .form-jurusan{
    background-color: rgb(172, 169, 175);
    }
    .form-kelas{
    background-color: rgb(172, 169, 175);
    }
    .form-keperluan{
    background-color: rgb(172, 169, 175);
    }
    .form-btn{
    background-color: rgb(172, 169, 175);
    }
    .form-kirim{
    background-color: rgb(172, 169, 175);
    }
</style>