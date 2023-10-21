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
    padding: 13px;

}
.headerText {
    color: #EFDE79;
    text-align: center;
    font-family: '';
    font-size: 30px;
    letter-spacing: 9px;
    font-style: 'bold';
    font-weight: 50;
    line-height: normal;
    display: flex;;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    font-family: 'italianno', cursive;

}

h4{
    color: #fff9c2;
    text-align: center;
    font-family: 'Charm', cursive;
    font-size: 20px;
    font-style: 'bold';
    font-weight: 60;
}
</style>