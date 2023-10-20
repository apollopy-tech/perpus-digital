<template>
    <div class="content">
        <form @submit.prevent="registerAnswer">
            <h1>Isi Data Pengunjung</h1>
            <p>
                <label for="name">Name</label>
                <input
                id="name"
                v-model="name"
                type="text"
                name="name"
                >
            </p>
            <p>
                <label for="name">Kategori</label>
                <input
                id="name"
                v-model="name"
                type="text"
                name="name"
                >
            </p>
            <p>
                <label for="name">Keperluan</label>
                <input
                id="name"
                v-model="name"
                type="text"
                name="name"
                >
            </p>
            <p>
                <label for="name">DD/MM/YYYY</label>
                <input
                id="name"
                v-model="name"
                type="date"
                name="name"
                >
            </p>
            <input type="submit" value="Submit">
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
const supabase = useSupabaseClient()
const datas = ref([])

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
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Bungee&display=swap');

.content {
    background-color: #A59663;
    width: 100%;
    height: 1024px;
    margin-top: 150px;
    left: 0;
    right: 0;

}
.slm{
    color: #FFF;
    text-align: center;
    font-family: 'Bungee', sans-serif;
    font-size: 64px;
    font-style: normal;
    font-weight: 400;
    line-height: normal;
}

.idk {
    color: #FFF;
    text-align: center;
    font-family: 'Bungee', sans-serif;
    font-size: 36px;
    font-style: normal;
    font-weight: 400;
    line-height: normal;
}
</style>