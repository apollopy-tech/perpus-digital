<template>
    <!--Input Data For DataBase-->
    <div class="content">
        <div class="container   ">
            <div class="row justify-content-center">
                <div class="col d-flex justify-content-center align-items-center text">
                    <div class="row d-flex align-content-center ">
                        <h3>Isi Data<br>Pengunjung</h3>
                    </div>
                    <div class="row m-5">
                        <NuxtLink class="text-center text-decoration-none py-2 btn-link" to="/history">
                            Riwayat Pengunjung
                        </NuxtLink>
                    </div>
                </div>
                
                <div class="col d-flex justify-content-center">
                    <form @submit.prevent="addData" autocomplete="off">
                        <div class="row "> 
                            <div class="col mb-4">
                                <input v-model.trim="name" type="text" class="form-control form-control-lg" id="name" placeholder="Nama..." required>
                            </div>
                        </div>
                        <div class="row" >
                            <div class="col mb-4">
                                <select v-model="kategori" @change="resetKelas" class="form-select" id="kategori" required>
                                    <option disabled value="">Kategori..</option>
                                    <option>Guru</option>
                                    <option>Siswa</option>
                                    <option>Staf</option>
                                    <option>Umum</option>
                                </select>
                            </div>
                        </div>
                        <div v-if="kategori == 'Siswa'"  class="row ">
                            <div class="col mb-4">
                                <select v-model="tingkat" id="tingkat" class="form-select" required>
                                    <option disabled value="">Tingkat..</option>
                                    <option>10</option>
                                    <option>11</option>
                                    <option>12</option>
                                </select>
                            </div>
                            <div class="col mb-4">
                                <select v-model="jurusan" id="jurusan" :disabled="!tingkat" class="form-select" required>
                                    <option disabled value="">Jurusan..</option>
                                    <option>PPLG</option>
                                    <option>TJKT</option>
                                    <option>TBSM</option>
                                    <option v-if="!(tingkat==12)">DKV</option>
                                    <option v-if="!(tingkat==12)">TOI</option>
                                </select>
                            </div>
                            <div class="col mb-4">
                                <select v-model="kelas" id="kelas" :disabled="!jurusan || jurusan=='TOI'" class="form-select" required>
                                    <option disabled value="">Kelas..</option>
                                    <option>1</option>
                                    <option>2</option>
                                    <option v-if="!(jurusan=='DKV')">3</option>
                                    <option v-if="!(jurusan=='DKV') && !(tingkat==12)">4</option>
                                </select>
                            </div>
                        </div>
                        <div class="row" >
                            <div class="col mb-4">
                                <select v-model="keperluan" class="form-select" id="kategori" required>
                                    <option disabled value="">Keperluan..</option>
                                    <option value="berkunjung">Berkunjung</option>
                                    <option value="meminjam">Meminjam Buku</option>
                                    <option value="membaca">Membaca di Tempat</option>
                                    <option value="mengembalikan">Mengembalikan Buku</option>
                                    <option >Lainnya</option>
                                </select>
                            </div>
                        </div>
                        <div v-if="keperluan == 'Lainnya'" class="row">
                                <div class="col mb-4">
                                    <input v-model.trim="lainnya" type="text" class="form-control form-control-lg" id="name" placeholder="Keperluan Lainnya..." required>
                                </div>
                        </div>
                        <div class="row d-flex justify-content-end me-2">
                            <input type="submit" class="btn" value="Kirim">
                        </div>
                        <!-- <div class="row d-flex justify-content-end">
                            <button id="btn">
                                <p id="btnText">Submit</p>
                                <div class="check-box">
                                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 50 50">
                                        <path fill="transparent" d="M14.1 27.2l7.1 7.2 16.7-16.8" />
                                    </svg>
                                </div>
                            </button>
                        </div> -->
                    </form>
                </div>
            </div>
            
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
const lainnya = ref('')
// const keperluanLain = ref('')
// const datas = ref([])

// Disabled Button
// const disablebtn = computed(() => {
//  const isSiswa = kategori.value === 'Siswa';
// })
// Add Data From Input To Database
async function addData(){
    kelasLengkap.value = `${tingkat.value} ${jurusan.value} ${kelas.value}`
    const { error } = await supabase
    .from('anggota')
    .insert([{
        kategori: kategori.value,
        kelas: kelasLengkap.value,
        nama: name.value,
        keperluan: keperluan.value && lainnya.value || keperluan.value || lainnya.value
    }])
    if (error) throw error
    else navigateTo('/history')
}

function resetKelas(e){
    if(e.target.value === 'Guru'||'Staf'||'Umum'){
        kelas.value= ''
        tingkat.value= ''
        jurusan.value= ''
    }
}

// const btn = ref(null);
// const btnText = ref(null);
//     btn.onclick = () => {
//         btnText.innerHTML = "Terkirim";
//         btn.classList.add("active");
//     };
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Bungee&family=Jomhuria&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Bungee&family=Chau+Philomene+One&family=Jomhuria&display=swap');

/* Visitors Style */
.content {
    background-image: url('@/assets/images/background.jpeg');
    width: 100%; 
    background-size: cover;
    padding: 150px 0;
}
.container {
    background:linear-gradient(90deg,#371502c1,#efdd79ad,#371502b4) ;
    border-radius: 100px    ;
    padding: 100px 0;
}
.text {
    flex-direction: column;
}
h3 {
    position: relative;
    text-shadow: 0px 4px 4px #efdd79b3;
    font-family: 'Jomhuria', serif;
    font-size: 120px;
    line-height: 80px; 
    letter-spacing: 5px;
    overflow: hidden;
    background: linear-gradient(90deg, #EFDE79, #ffe23f, #f6ff00,  #ffd900, #EFDE79);
    background-repeat: no-repeat;
    background-size: 84%;
    background-clip: text;
    /* font-weight: 80px; */
    animation: animate 5s linear infinite;
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
/* 
button{
    width: 270px;
    height: 80px;
    border: none;
    outline: none;
    background: #2f2f2f;
    color: #fff;
    font-size: 22px;
    border-radius: 40px;
    text-align: center;
    box-shadow: 0 6px 20px -5px rgba(0,0,0,0.4);
    position: relative;
    overflow: hidden;
    cursor: pointer;
}

.check-box{
    width: 80px;
    height: 80px;
    border-radius: 40px;
    box-shadow: 0 0 12px -2px rgba(0,0,0,0.5);
    position: absolute;
    top: 0;
    right: -40px;
    opacity: 0;
}

.check-box svg{
    width: 40px;
    margin: 20px;
}

svg path{
    stroke-width: 3;
    stroke: #fff;
    stroke-dasharray: 34;
    stroke-dashoffset: 34;
    stroke-linecap: round;
}

.active{
    background: #ff2b75;
    transition: 1s;
}

.active .check-box{
    right: 0;
    opacity: 1;
    transition: 1s;
}

.active p{
    margin-right: 125px;
    transition: 1s;
}

.active svg path{
    stroke-dashoffset: 0;
    transition: 1s;
    transition-delay: 1s;
}
*/
.btn-link {
    width: 15rem;
    height: 40px;
    color:  #ffee8f ;  
    font-size: larger;
    background: linear-gradient(180deg, #ffe75f,#ceaf4a,#ceaf4a,#ffe75f);
    filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
    border-radius: 50px;
    border-style: hidden; 
    transform: rotate(-0.800deg);
    font-family: 'Chau Philomene One', sans-serif;
    transition: background-color ,color ,0.3s ease ;
}

.btn-link:hover{
    background: linear-gradient(180deg, #ceaf4a, #ffe75f,#ceaf4a);
    color: rgb(100,100,0);
}
.form {
    margin-right: 14%;
    margin-top:  7%;
}
.layer{
    width: 30rem;
    height: 30rem;
    background-color: #655602;
    opacity: 0.3;
}
#name {
    width: 25rem;
    height: 50px;
    font-size: 25px;
    letter-spacing: 2px;
    background-color: #fff9c2;
    filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
    border-radius: 50px;
    border-style: hidden;
    font-family: 'Chau Philomene One', sans-serif;
}
#kategori {
    width: 25rem;
    height: 55px;   
    font-size: 25px;
    letter-spacing: 2px;
    background-color: #fff9c2;
    filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
    border-radius: 50px;
    border-style: hidden;
    font-family: 'Chau Philomene One', sans-serif;
}
#kelas {
    width: 100px;
    height: 50px;
    font-size: 19px;
    letter-spacing: 1px;
    background-color: #fff9c2;
    filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
    border-radius: 50px;
    border-style: hidden;
    font-family: 'Chau Philomene One', sans-serif;
}
#tingkat {
    width: 120px;
    height: 50px;
    font-size: 19px;
    letter-spacing: 1px;
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
    letter-spacing: 1px;
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
    font-size: 25px;
    letter-spacing: 2px;
    padding-left: 15px;
    background-color: #fff9c2;
    filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
    border-radius: 50px;
    border-style: hidden;
    font-family: 'Chau Philomene One', sans-serif;
}
/* End Visitor Style */

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
