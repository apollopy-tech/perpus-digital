<template>
<div class="content">
    <h1>Isi Data Pengunjung</h1>
    <form>
    <p>
        <label for="name">Nama</label>
        <input id="name" v-model="name" type="text" name="name" />
    </p>
    <p>
        <input id="kategori" v-model="kategori" type="text" name="kategori" placeholder="Kategori" />
    </p>
    <p>
        <label for="keperluan">Keperluan</label>
        <input id="keperluan" v-model="keperluan" type="text" name="keperluan" />
    </p>
    <input type="submit" value="Submit" />
    </form>
</div>

<div v-for="(anggota, index) in datas" :key="anggota.id">
    <div>{{ index + 1 }}</div>
    <div>{{ anggota.nama }}</div>
    <div>{{ anggota.kategori }}</div>
    <div>{{ anggota.keperluan }}</div>
    <div>{{ anggota.tanggal }}</div>
</div>
</template>

<script setup>
const supabase = useSupabaseClient();
const datas = ref([]);

async function getData() {
const { data, error } = await supabase.from("anggota").select();
if (error) throw error;
if (data) {
    console.log(data);
    datas.value = data;
}
}

onMounted(() => {
getData();
});
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Bungee&display=swap");

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

#name {
    width: 350px;
    height: 50px;
    font-size: 30px;
}
#kategori {
    width: 350px;
    height: 50px;
    font-size: 30px;
}
#keperluan {
    width: 350px;
    height: 50px;
    font-size: 30px;
}
#tanggal{
    width: 350px;
    height: 50px;
    font-size: 30px;
}
</style>