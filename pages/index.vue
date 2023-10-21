<template>
    <div class="content">
        <h3>Isi Data <br>Pengunjung</h3>
        <form @submit.prevent="addData" >
            <p>
                <input id="name" v-model="name" type="text" name="name" placeholder="Nama..." required/>
            </p>
            <p>
                <input id="kategori" v-model="kategori" type="text" name="kategori" placeholder="Kategori..." required />
            </p>
            <p>
                <input id="keperluan" v-model="keperluan" type="text" name="keperluan" placeholder="Keperluan..." required/>
            </p>    
            <button class="btn">Submit</button>
        </form>
    </div>


    <div class="showData">
        <h1>Riwayat Pengunjung</h1>
        <table>
            <thead>
                <tr>
                    <th class="no">No</th>
                    <th class="nama">Nama</th>
                    <th class="kategori">Kategori</th>
                    <th class="keperluan">Keperluan</th>
                    <th class="tanggal">Tanggal</th>
                </tr>
            </thead>
            <tbody v-for="(anggota, index) in datas" :key="anggota.id " class="tableData">
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
const datas = ref([])
const name = ref('')
const kategori = ref('')
const keperluan = ref('')

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

.content {
    background-color: #a58c39;
    width: 100%;
    height: 700px;
    margin-top: 150px;
    display: flex;
    justify-content: space-evenly;
    flex-direction: row;
    flex-wrap: wrap;
    align-content: center;
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

.showData {
    background-color: #483800ec;
    display: flex;
    flex-direction: column;
}

h1{
    position: relative;
    text-shadow: 0px 4px 4px rgba(255, 246, 121, 0.25);
    font-family: 'Italianno', cursive;
    text-align: center;
    font-size: 50px;
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
table {
    border: 2px solid rgb(149, 135, 29);
    border-collapse: collapse;
    text-align: center;
    font-family: 'Charm';
    letter-spacing: 2px;
    font-size: 18px;
    margin-left: 30px;
    margin-right: 30px;
    margin-bottom: 25px;
    color: #372f00;
}
td{
    border: 0.3px solid rgb(149, 135, 29);
    color: rgb(255, 242, 124);
    border-collapse: collapse;
    
}

thead ,th{
    padding: 20px 100px;
    border: 2px solid rgb(149, 135, 29);
    font-style: 'bold';
    color: rgb(255, 238, 124);
    font-size: 25px;
}

.no {
    padding: 25px;
}
</style>