<template>
    <!--Input Data For DataBase-->
    <div class="content">
        <div class="container">
            <div class="row justify-content-center">
                <div class="col d-flex justify-content-center align-items-center">
                    <h3>Isi Data<br>Pengunjung</h3>
                </div>
                <div class="col d-flex justify-content-center">
                    <form @submit.prevent="addData">
                        <div class="row">
                            <div class="col mb-4">
                                <input v-model="name" type="text" class="form-control form-control-lg" id="name" placeholder="Nama..." required>
                            </div>
                        </div>
                        <div class="row" >
                            <div class="col mb-4">
                                <select v-model="kategori" class="form-select" id="kategori">
                                    <option disabled value="">Kategori..</option>
                                    <option>Guru</option>
                                    <option>Siswa</option>
                                    <option>Staf</option>
                                    <option>Umum</option>
                                </select>
                            </div>
                        </div>
                        <div v-if="kategori == 'Siswa'" class="row ">
                            <div class="col mb-4">
                                <select v-model="tingkat" id="tingkat" class="form-select">
                                    <option disabled value="">Tingkat..</option>
                                    <option>10</option>
                                    <option>11</option>
                                    <option>12</option>
                                </select>
                            </div>
                            <div class="col mb-4">
                                <select v-model="jurusan" id="jurusan" :disabled="!tingkat" class="form-select">
                                    <option disabled value="">Jurusan..</option>
                                    <option>PPLG</option>
                                    <option>TJKT</option>
                                    <option>TBSM</option>
                                    <option v-if="!(tingkat==12)">DKV</option>
                                    <option v-if="!(tingkat==12)">TOI</option>
                                </select>
                            </div>
                            <div class="col mb-4">
                                <select v-model="kelas" id="kelas" :disabled="!jurusan || jurusan=='TOI'" class="form-select">
                                    <option disabled value="">Kelas..</option>
                                    <option>1</option>
                                    <option>2</option>
                                    <option v-if="!(jurusan=='DKV')">3</option>
                                    <option v-if="!(jurusan=='DKV') && !(tingkat==12)">4</option>
                                </select>
                            </div>
                        </div>
                        <div class="row">
                            <div class="col mb-4">
                                <input v-model="keperluan" type="text" class="form-control form-control-lg" id="keperluan" placeholder="Keperluan..." required>
                            </div>
                        </div>
                        <div class="row float-end">
                            <button class="btn">Submit</button>
                        </div>
                    </form>
                </div>
            </div>
        
        </div>
    </div>

    <!--Showing Data Tables-->
    <div class="showData">
        <h1>Riwayat<br>Pengunjung</h1>
        <div class="table-responsive">
            <div class="text-center fs-4 m-3 ">Menampilkan {{ datas.length }} data</div>
            <table class="table table-responsive">
                <thead>
                    <tr>
                        <th class="no">No</th>
                        <th class="nama">Nama</th>
                        <th class="kategori">Kategori</th>
                        <th class="kelas">Kelas</th>
                        <th class="keperluan">Keperluan</th>
                        <th class="tanggal">Tanggal</th>
                </tr>
            </thead>
            <tbody v-for="(anggota, index) in datas" :key="anggota.id " class="">
                <td>{{ index + 1 }}</td>
                <td>{{ anggota.nama }}</td>
                <td>{{ anggota.kategori }}</td>
                <td>{{ anggota.kelas }}</td>
                <td>{{ anggota.keperluan }}</td>
                <td>{{ anggota.tanggal }}</td>
            </tbody>
        </table>
    </div>
    </div>
</template>

<script setup>

const supabase = useSupabaseClient()
const name = ref('')
const kategori = ref('')
const keperluan = ref('')
const tingkat = ref('')
const jurusan = ref('')
const kelas = ref('')
const kelasLengkap = ref('')
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


// Add Data From Input To Database
async function addData(){
    kelasLengkap.value = `${tingkat.value} ${jurusan.value} ${kelas.value}`
    const { error } = await supabase
    .from('anggota')
    .insert([{
        kategori: kategori.value,
        kelas: kelasLengkap.value,
        nama: name.value,
        keperluan: keperluan.value
    }])
    if (error) throw error
    else getData()
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Bungee&family=Jomhuria&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Bungee&family=Chau+Philomene+One&family=Jomhuria&display=swap');

/* Visitors Style */
.content {
    background-color: #a58c39;
    width: 100%;
    padding: 300px 0;
}

h3 {
    position: relative;
    text-shadow: 0px 4px 4px rgba(32, 30, 0, 0.25);
    font-family: 'Jomhuria', serif;
    font-size: 140px;
    line-height: 90px; 
    letter-spacing: 7px;
    overflow: hidden;
    background: linear-gradient(90deg, #7d6f24, #f6ff00, #EFDE79);
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
        background-position: -500%;
    }
    100% {
        background-position: 1000%;
    }
}
    
.btn {
    width: 100px;
    height: 35px;
    color: #000000;
    background-color: #feffd3;
    filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
    border-radius: 50px;
    border-style: hidden; 
    transform: rotate(-0.800deg);
    font-family: 'Chau Philomene One', sans-serif;
    transition: background-color ,color ,1s ease ;
}

.btn:hover{
    background-color: #655602 ;
    color: #ffffff;
}
form {
    margin-top: 25px;
}
#name {
    width: 25rem;
    height: 50px;
    font-size: 20px;
    background-color: #fff9c2;
    filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
    border-radius: 50px;
    border-style: hidden;
    font-family: 'Chau Philomene One', sans-serif;
}
#kategori {
    width: 25rem;
    height: 50px;
    font-size: 20px;
    background-color: #fff9c2;
    filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
    border-radius: 50px;
    border-style: hidden;
    font-family: 'Chau Philomene One', sans-serif;
}
#kelas {
    width: 100px;
    height: 50px;
    font-size: 20px;
    background-color: #fff9c2;
    filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
    border-radius: 50px;
    border-style: hidden;
    font-family: 'Chau Philomene One', sans-serif;
}
#tingkat {
    width: 120px;
    height: 50px;
    font-size: 20px;
    background-color: #fff9c2;
    filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
    border-radius: 50px;
    border-style: hidden;
    font-family: 'Chau Philomene One', sans-serif;
}
#jurusan {
    width: 130px;
    height: 50px;
    font-size: 20px;
    background-color: #fff9c2;
    filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
    border-radius: 50px;
    border-style: hidden;
    font-family: 'Chau Philomene One', sans-serif;
}
#keperluan {
    width: 25rem;
    height: 50px;
    font-size: 20px;
    padding-left: 15px;
    background-color: #fff9c2;
    filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
    border-radius: 50px;
    border-style: hidden;
    font-family: 'Chau Philomene One', sans-serif;
}
/* End Visitor Style */

/* History Style */
.showData {
    background-color: #483800ec;
    display: flex;
    flex-direction: column;
    padding: 100px 50px 50px;
}

.table-responsive{
    border: 2px solid #A59663;
    font-family: 'Chau Philomene One', sans-serif;
    color: wheat;
    letter-spacing: 3px;

}
thead {
    border: 2px solid #A59663;
    color: #655602;
    height: 50px;
    font-size: 28px;
    background-color: #ecdf87;
}


tbody {
    border: 1px solid;
    font-size: 25px;
}
h1{
    position: relative;
    text-shadow: 0px 4px 4px rgba(255, 242, 59, 0.363);
    font-family: 'Jomhuria', serif;
    text-align: center;
    font-size: 100px;
    line-height: 65px; 
    letter-spacing: 10px;
    overflow: hidden;
    background: linear-gradient(90deg, #685b11, #f6ff00, #ffef96);
    background-repeat: no-repeat;
    background-size: 90%;
    background-clip: text;
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

/* Style For Mobile Screen */
@media (max-width=450px) {
    .btn {
    width: 100px;
    height: 35px;
    color: #000000;
    background-color: #feffd3;
    filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
    border-radius: 50px;
    border-style: hidden; 
    transform: rotate(-0.800deg);
    font-family: 'Chau Philomene One', sans-serif;
    transition: background-color ,color ,1s ease ;
    }

    .btn:hover{
        background-color: #655602 ;
        color: #ffffff;
    }
    .content{
        background-color: #a58c39;
        width: 100%;
    }
    #name {
        width: 10rem;
        height: 50px;
        font-size: 20px;
        background-color: #fff9c2;
        filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
        border-radius: 50px;
        border-style: hidden;
        font-family: 'Chau Philomene One', sans-serif;
    }
    #kategori {
        width: 15rem;
        height: 50px;
        font-size: 20px;
        background-color: #fff9c2;
        filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
        border-radius: 50px;
        border-style: hidden;
        font-family: 'Chau Philomene One', sans-serif;
    }
    #kelas {
        width: 90px;
        height: 50px;
        font-size: 20px;
        background-color: #fff9c2;
        filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
        border-radius: 50px;
        border-style: hidden;
        font-family: 'Chau Philomene One', sans-serif;
    }
    #tingkat {
        width: 100px;
        height: 50px;
        font-size: 20px;
        background-color: #fff9c2;
        filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
        border-radius: 50px;
        border-style: hidden;
        font-family: 'Chau Philomene One', sans-serif;
    }
    #jurusan {
        width: 100px;
        height: 50px;
        font-size: 20px;
        background-color: #fff9c2;
        filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
        border-radius: 50px;
        border-style: hidden;
        font-family: 'Chau Philomene One', sans-serif;
    }
    #keperluan {
        width: 20rem;
        height: 50px;
        font-size: 20px;
        padding-left: 15px;
        background-color: #fff9c2;
        filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
        border-radius: 50px;
        border-style: hidden;
        font-family: 'Chau Philomene One', sans-serif;
    }
    .showData {
    background-color: #483800ec;
    display: flex;
    flex-direction: column;
}
}

</style>
