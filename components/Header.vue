<template>
    <div>
        <div class="nav-container">
            <img src="@/assets/images/companylogo.png" class="company"/>
            <div class="headerText">
                <h1>PERPUSTAKAAN DIGITAL</h1>
                <h4>SMK NEGERI 4 TASIKMALAYA</h4>
            </div>
            <img src="@/assets/images/perpusnasional.png" class="perpusnasional"/>
            <img src="@/assets/images/logosmk.png" class="smk"/>
        </div>
    </div>
</template>

<script setup>

</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Bungee&display=swap');

*{
margin: 0;
}
.nav-container {
    background-color:#413304;
    width: 100%;
    height: 150px;
    display: flex;
    justify-content: space-evenly;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
}

.company {
    width: 257.178px;
    height: 89px;
    padding: 30px;
}

.perpusnasional{
    width: 150.104px;
    height: 152px;
}
.smk{
    width: 111.077px;
    height: 126px;
    padding: 20px;
}
.headerText {
    color: #EFDE79;
    text-align: center;
    font-family: '';
    font-size: 20px;
    font-style: normal;
    font-weight: 50;
    line-height: normal;
    display: flex;;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    font-family: 'Bungee', sans-serif;
}

h4{
    color: #FFF;
    text-align: center;
    font-family: 'Bungee';
    font-size: 20px;
    font-style: normal;
    font-weight: 50;
    line-height: normal;
}
</style>