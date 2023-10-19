<template>
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

</style>