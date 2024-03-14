    <template>
    <!--Showing Data Tables-->
    <div class=" showData">
        <div class="layer py-5">
            <h1 class="display-4 mb-5 text-center">Riwayat<br>Pengunjung</h1>
                <div class="fs-4 d-flex justify-content-around align-items-center p-2 tbl">
                    <NuxtLink class="btn-link text-center text-decoration-none" to="/">
                        Isi Data Pengunjung
                    </NuxtLink>
                    <div class="layer-rounded">Menampilkan {{ datas.length }} data</div>
                </div>
            </div>
            <div class="table table-responsive">
            <table class="table table-bordered table-striped-color table-hover my-5">
                <thead class="headTable">
                    <tr>
                        <th class="no text-center">No</th>
                        <th class="nama text-center">Nama</th>
                        <th class="kategori text-center">Kategori</th>
                        <th class="kelas text-center">Kelas</th>
                        <th class="keperluan text-center">Keperluan</th>
                        <th colspan="2" class="tanggal text-center">Waktu</th>
                    </tr>
                </thead>
                <tbody v-for="(anggota, index) in datas" :key="anggota.id " class="bodyTable">
                    <tr>
                        <td>{{ index + 1 }}</td>
                        <td>{{ anggota.nama }}</td>
                        <td>{{ anggota.kategori }}</td>
                        <td>{{ anggota.kelas }}</td>
                        <td>{{ anggota.keperluan }}</td>
                        <td>{{ anggota.tanggal.split('T')[0]}}</td>
                        <td>{{ anggota.tanggal.split('T')[1].split('.')[0]}}</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script setup>
const supabase = useSupabaseClient()
// const name = ref('')
// const kategori = ref('')
// const keperluan = ref('')
// const tingkat = ref('')
// const jurusan = ref('')
// const kelas = ref('')
// const kelasLengkap = ref('')
const datas = ref([])


// Get Data From DataBase
async function getData() {
    
    const { data, error } = await supabase
    .from("anggota")
    .select()
    .order('tanggal', { ascending: false })
    if (error) throw error
    if (data) {
        // console.log(data)
        datas.value = data
    } 
}


onMounted(() => {
    getData()
})
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Bungee&family=Jomhuria&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Bungee&family=Chau+Philomene+One&family=Jomhuria&display=swap');

/* History Style */
.showData {
    /* background-color: #391800fd; */
    display: flex;
    background-image: url('@/assets/images/background.jpeg');
    background-size: cover;
    flex-direction: column;
    padding: 120px 50px 0;
}

.layer {
    background: linear-gradient(90deg,#371502c1,#efdd79ad,#371502b4);
    border-radius: 100px;
}
.table-responsive{
    font-family: 'Chau Philomene One', sans-serif;
    color: wheat;
    letter-spacing: 3px;
}
.layer-rounded{
    background-color: #655602;
    width: 18rem;
    filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
    height: 40px;
    color: #ffffff ;
    text-align: center;
    font-family: 'Chau Philomene One', sans-serif;
    border-radius: 50px;
}
.headTable {
    border: 2px solid #A59663;
    color: #655602;
    height: 50px;
    font-size: 28px;
    background-color: #ecdf87;
}

.btn-link {
    width: 20rem;
    height: 40px;
    color: #000000;
    background-color: #dee083;
    filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
    border-radius: 50px;
    border-style: hidden; 
    transform: rotate(-0.800deg);
    font-family: 'Chau Philomene One', sans-serif;
    transition: background-color ,color ,1s ease ;
}
.btn-link:hover{
    background-color: #655602 ;
    color: #ffffff;
}
.bodyTable {
    border: 1px solid #655602;
    font-size: 22px;
    background-color: #dee083;
    letter-spacing: 3px;
    color: #484848;
    font-weight: 10px;
    text-align: center;
}

h1{
    position: relative;
    text-shadow: 0px 4px 4px #8e7900b7;
    font-family: 'Jomhuria', serif;
    font-size: 120px;
    line-height: 80px; 
    letter-spacing: 5px;
    overflow: hidden;
    background: linear-gradient(90deg,  #8e7900, #EFDE79,#f6ff00, #EFDE79,#8e7900);
    background-repeat: no-repeat;
    background-size: 90%;
    background-clip: text;
    /* font-weight: 80px; */
    animation: animate 4s linear infinite;
    -webkit-background-clip: text;
    -webkit-text-fill-color: rgba(94, 86, 36, 0);
}

@keyframes animate {
    0% {
        background-position: -1000%;
    }
    100% {
        background-position: 1000%;
    }
}
/* End History Style */


</style>