<template>
    <div class="main1">
        <a class="btn" :class="show">
            <router-link to="/about">перейти к тесту</router-link>
        </a>
    </div>
</template>

<script>
export default {
    data: () => ({
        show: false 
    })
}
</script>

<style>
.main1{
    display: flex;
    justify-content: center ;
    align-items: center;
    min-height: 100vh;

    background-image: url(https://i.stack.imgur.com/SvWWN.png);

}
body{
    margin: 0;
    padding: 0;
}
.show {
    display: none;
}
.btn a{
    color: #ffffff;
    text-decoration: none;
    font-size: 20px;

}
.btn{
    font-family: monospace;
    background: linear-gradient(to left, #355C7D,#6C5B7B,#C06C84);
    text-decoration: none;
    padding: 20px 70px;
    border-radius: 10px;
    background-size: 200%;
    transition: .5s;
    color: white;

}   
.btn:hover {
    background-position: right;
    
}
</style>