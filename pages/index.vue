<template>
    <!--Input Data For DataBase-->
    <div class="content">
        <h3>Isi Data <br>Pengunjung</h3>
        <form @submit.prevent="addData" >
            <div class="row">
                <div class="col-sm-10">
                    <input v-model="name" type="text" class="form-control form-control-lg" id="name" placeholder="Nama..." required>
                </div>
            </div>
            <div class="row">
                <div class="col-sm-10">
                    <input v-model="kategori" type="text" class="form-control form-control-lg" id="kategori" placeholder="Kategori..." required>
                </div>
            </div>
            <div class="row">
                <div class="col-sm-10">
                    <input v-model="keperluan" type="text" class="form-control form-control-lg" id="keperluan" placeholder="Keperluan..." required>
                </div>
            </div>  
            <button class="btn">Submit</button>
        </form>
    </div>

    <!--Showing Data Tables-->
    <div class="showData">
        <h1>Riwayat Pengunjung</h1>
        <table class="table-responsive">
            <thead>
                <tr>
                    <th class="no">No</th>
                    <th class="nama">Nama</th>
                    <th class="kategori">Kategori</th>
                    <th class="keperluan">Keperluan</th>
                    <th class="tanggal">Tanggal</th>
                </tr>
            </thead>
            <tbody v-for="(anggota, index) in datas" :key="anggota.id ">
                <td>{{ index + 1 }}</td>
                <td>{{ anggota.nama }}</td>
                <td>{{ anggota.kategori }}</td>
                <td>{{ anggota.keperluan }}</td>
                <td>{{ anggota.tanggal }}</td>
            </tbody>
        </table>
    </div>
</template>

<script setup>

const supabase = useSupabaseClient()
const name = ref('')
const kategori = ref('')
const keperluan = ref('')
const datas = ref([])

// Get Data From DataBase
async function getData() {
    const { data, error } = await supabase
    .from("anggota")
    .select()
    if (error) throw error
    if (data) {
        console.log(data)
        datas.value = data
    } 
}


onMounted(() => {
    getData()
})


// Add Data From Input To Database
async function addData(){
    const { error } = await supabase
    .from('anggota')
    .insert([{
        kategori: kategori.value,
        nama: name.value,
        keperluan: keperluan.value
    }])
    if (error) throw error
    else getData()
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Bungee&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Italianno&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Charm:wght@700&family=Italianno&display=swap');

/* Visitors Style */
.content {
    background-color: #a58c39;
    width: 100%;
    height: 700px;
    padding-top: 150px;
    display: flex;
    justify-content: space-evenly;
    flex-direction: row;
    flex-wrap: wrap;
    align-content: center;
}

.row {
    margin: 15px;
}
h3 {
    position: relative;
    text-shadow: 0px 4px 4px rgba(58, 54, 0, 0.25);
    font-family: 'Italianno', cursive;
    font-size: 70px;
    letter-spacing: 7px;
    overflow: hidden;
    background: linear-gradient(90deg, #7d6f24, #f6ff00, #EFDE79);
    background-repeat: no-repeat;
    background-size: 80%;
    animation: animate 3.8s linear infinite;
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
    height: 30px;
    color: #000000;
    background-color: #feffd3;
    filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
    border-radius: 50px;
    border-style: hidden; 
    float: right;
    transform: rotate(-0.800deg);
    font-family: 'Charm';
    transition: background-color ,color ,1s ease ;
    margin: 10px 30px ;
}

.btn:hover{
    background-color: #655602 ;
    color: #ffffff;
}
form {
    margin-top: 25px;
}
#name {
    width: 335px;
    height: 50px;
    font-size: 20px;
    padding-left: 15px;
    background-color: #fff9c2;
    filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
    border-radius: 50px;
    border-style: hidden;
    font-family: 'Charm';
}
#kategori {
    width: 335px;
    height: 50px;
    font-size: 20px;
    padding-left: 15px;
    background-color: #fff9c2;
    filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
    border-radius: 50px;
    border-style: hidden;
    font-family: 'Charm';
}
#keperluan {
    width: 335px;
    height: 50px;
    font-size: 20px;
    padding-left: 15px;
    background-color: #fff9c2;
    filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
    border-radius: 50px;
    border-style: hidden;
    font-family: 'Charm';
}
/* End Visitor Style */

/* History Style */
.showData {
    background-color: #483800ec;
    display: flex;
    flex-direction: column;
    padding: 60px 5px 5px 0px;
}

.table-responsive{
    border: 2px solid #A59663;
    font-family: 'Charm', cursive;
    color: wheat;
    margin: 15px;
    letter-spacing: 3px;

}
thead {
    border: 2px solid #A59663;
    color: #655602;
    font-size: 22px;
    background-color: #ecdf87;
}


tbody {
    border: 1px solid;
}
h1{
    position: relative;
    text-shadow: 0px 4px 4px rgba(255, 246, 121, 0.25);
    font-family: 'Italianno', cursive;
    text-align: center;
    font-size: 70px;
    letter-spacing: 7px;
    overflow: hidden;
    background: linear-gradient(85deg, #685b11, #f6ff00, #ffef96);
    background-repeat: no-repeat;
    background-size: 80%;
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
@media (max-width=480px) {
}
</style>