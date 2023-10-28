<template>
    <div>
        <div class="nav-container">
            <img src="@/assets/images/companylogo.png" class="company"/>
            <div class="headerText">
                <h1>Perpustakaan Digital</h1>
                <h4>SMK Negeri 4 Tasikmalaya</h4>
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
@import url('https://fonts.googleapis.com/css2?family=Italianno&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Charm:wght@700&family=Italianno&display=swap');

*{
margin: 0;
z-index: 1;
}
.nav-container {
    background-color:#413304;
    width: 100%;
    height: 150px;
    display: flex;
    justify-content: space-evenly;
    align-items: center;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
}

.company {
    width: 257.178px;
    height: 90px;
}

.perpusnasional{
    width: 150.104px;
    height: 152px;
}
.smk{
    width: 111.077px;
    height: 126px;

}
h1 {
    color: #EFDE79;
    text-align: center;
    font-family: '';
    font-size: 55px;
    letter-spacing: 9px;
    font-weight: 50;
    line-height: normal;
    font-family: 'italianno', cursive;

}

h4{
    color: #fff9c2;
    text-align: center;
    font-family: 'Charm', cursive;
    font-size: 20px;
    letter-spacing: 4px;
    font-style: 'bold';
    font-weight: 60;
}

@media (max-width: 520px) {
    .nav-container {
        background-color:#413304;
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
    
    .perpusnasional{
        width: 60.104px;
        height: 59px;
    }
    .smk{
        width: 46.077px;
        height: 50px;
    
    }
    h1 {
        color: #EFDE79;
        text-align: center;
        font-family: '';
        font-size: 26px;
        letter-spacing: 4px;
        font-style: 'bold';
        font-family: 'italianno', cursive;
    
    }
    
    h4{
        color: #fff9c2;
        text-align: center;
        font-family: 'Charm', cursive;
        font-size: 13px;
        letter-spacing: 2px;
        font-style: 'bold';
        font-weight: 60;
    }
}
@media (max-width: 820px) {
    .nav-container {
        background-color:#413304;
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
    
    .perpusnasional{
        width: 100.104px;
        height: 90px;
    }
    .smk{
        width: 80.077px;
        height: 80px;
    
    }
    h1 {
        color: #EFDE79;
        text-align: center;
        font-family: '';
        font-size: 45px;
        letter-spacing: 4px;
        font-style: 'bold';
        font-family: 'italianno', cursive;
    
    }
    
    h4{
        color: #fff9c2;
        text-align: center;
        font-family: 'Charm', cursive;
        font-size: 13px;
        letter-spacing: 2px;
        font-style: 'bold';
        font-weight: 60;
    }
}
</style>