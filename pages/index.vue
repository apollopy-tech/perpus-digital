<template>
<div class="content">
    <h1>Isi Data Pengunjung</h1>
    <form @submit.prevent="addData">
    <p>
        <input id="name" v-model="name" type="text" name="name" placeholder="Nama"/>
    </p>
    <p>
        <input id="kategori" v-model="kategori" type="text" name="kategori" placeholder="Kategori" />
    </p>
    <p>
        <input id="keperluan" v-model="keperluan" type="text" name="keperluan" placeholder="Keperluan" />
    </p>
    <input type="submit" value="Submit" class="btn"/>
    </form>
</div>
    
    <table>
        <thead>
        <tr>
            <th>No</th>
                <th>Nama</th>
                <th>Kategori</th>
                <th>Keperluan</th>
                <th>Tanggal</th>
            </tr>
        </thead>
        <tbody v-for="(anggota, index) in datas" :key="anggota.id">
            <th>{{ index + 1 }}</th>
            <th>{{ anggota.nama }}</th>
            <th>{{ anggota.kategori }}</th>
            <th>{{ anggota.keperluan }}</th>
            <th>{{ anggota.tanggal }}</th>
        </tbody>
    </table>
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

.content {
background-color: #a59663;
width: 100%;
height: 700px;
margin-top: 150px;
display: flex;
justify-content: space-evenly;
flex-direction: row;
flex-wrap: wrap;
align-content: center;
left: 0;
right: 0;
}
h1 {
color: #fff;
text-align: center;
font-family: "Bungee", sans-serif;
font-size: 45px;
font-style: normal;
font-weight: 100;
line-height: normal;
}

.btn {
    width: 100px;
    height: 25px;
    float: right;
    background-color: #009171;
    box-shadow: 2px 2px 3px 1px ;
    border-radius: 10px;
}
#name {
    width: 350px;
    height: 50px;
    font-size: 30px;
    background-color: #c2c2c2;
    box-shadow: 2px 2px 3px 1px ;
}
#kategori {
    width: 350px;
    height: 50px;
    font-size: 30px;
    background-color: #c2c2c2;
    box-shadow: 2px 2px 3px 1px ;
}
#keperluan {
    width: 350px;
    height: 50px;
    font-size: 30px;
    box-shadow: 2px 2px 3px 1px ;
    background-color: #c2c2c2;
}
</style>