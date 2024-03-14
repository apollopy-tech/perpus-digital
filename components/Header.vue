<template>
    <div class="nav-container">
        <img src="@/assets/images/companylogo.png" class="company"/>
        <div class="headerText">
            <h1>Perpustakaan Digital</h1>
            <h4>SMK Negeri 4 Tasikmalaya</h4>
        </div>
        <img src="@/assets/images/logosmk.png" class="smk"/>
    </div>
</template>

<script setup>

</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Bungee&family=Jomhuria&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Bungee&family=Chau+Philomene+One&family=Jomhuria&display=swap');

*{
margin: 0;
z-index: 1;
}
.nav-container {
    background-color:#371502;
    width: 100%;
    height: 170px;
    display: flex;
    justify-content: space-evenly;
    align-items: center;
    top: 0;
    left: 0;
    right: 0;
}

.company {
    width: 257.178px;
    height: 90px;
    margin: 0 10px;
}

.smk{
    width: 111.077px;
    height: 126px;
    margin: 0 30px;

}
h1 {
    color: #EFDE79;
    text-align: center;
    font-family: '';
    font-size: 120px;
    letter-spacing: 9px;
    line-height: 60px;
    font-family: 'Jomhuria', serif;

}

h4{
    color: #fff9c2;
    text-align: center;
    font-family: 'Chau Philomene One', sans-serif;
    font-size: 30px;
    letter-spacing: 4px;
    font-style: 'bold';
    font-weight: 60;
}

@media (max-width: 520px) {
    .nav-container {
        background-color:#371502;
        width: 100%;
        height: 80px;
        display: flex;
        justify-content: space-evenly;
        align-items: center;
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
    }
    
    .company {
        width: 100.178px;
        height:30px;
    }
    
    .smk{
        width: 46.077px;
        height: 50px;
    
    }
    h1 {
        color: #EFDE79;
        text-align: center;
        line-height: 60px;
        font-size: 26px;
        letter-spacing: 4px;
        font-style: 'bold';
        font-family: 'Jomhuria', serif;
    
    }
    
    h4{
        color: #fff9c2;
        text-align: center;
        font-family: 'Chau Philomene One', sans-serif;
        font-size: 13px;
        letter-spacing: 2px;
        line-height: 60px;
        font-style: 'bold';
        font-weight: 60;
    }
}
@media (max-width: 820px) {
    .nav-container {
        background-color:#371502;
        width: 100%;
        height: 130px;
        display: flex;
        justify-content: space-evenly;
        align-items: center;
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
    }
    
    .company {
        width: 160.178px;
        height:50px;
    }
    .smk{
        width: 80.077px;
        height: 90px;
    
    }
    h1 {
        color: #EFDE79;
        text-align: center;
        line-height: 40px;
        font-size: 60px;
        font-weight: 50px;
        letter-spacing: 4px;
        font-style: 'bold';
        font-family: 'Jomhuria', serif;
    
    }
    
    h4{
        color: #fff9c2;
        text-align: center;
        font-family: 'Chau Philomene One', sans-serif;
        font-size: 20px;
        letter-spacing: 2px;
        font-style: 'bold';
        font-weight: 60;
        line-height: 40px;
    }
}
@media (max-width: 450px) {
    .nav-container {
        background-color:#371502;
        width: 100%;
        height: 100px;
        display: flex;
        justify-content: space-evenly;
        align-items: center;
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
    }
    
    .company {
        width: 80.178px;
        height:30px;
    }
    .smk{
        width: 40.077px;
        height: 40px;
    
    }
    h1 {
        color: #EFDE79;
        text-align: center;
        line-height: 20px;
        font-size: 40px;
        letter-spacing: 4px;
        font-family: 'Jomhuria', serif;
    
    }
    
    h4{
        color: #fff9c2;
        text-align: center;
        font-family: 'Chau Philomene One', sans-serif;
        font-size: 15px;
        letter-spacing: 2px;
        font-weight: 20;
        line-height: 20px;
    }
}
</style>
