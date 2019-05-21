<template>
    <div class='left-nav'>
        <ul>
            <li>
                <router-link to='/'>
                    <i class='icon iconfont icon-goumai1'></i>
                    <div>收银</div>
                </router-link>
                
            </li>
            <li>
                <i class='icon iconfont icon-dianpu'></i>
                <div>店铺</div>
            </li>
            <li>
                <i class='icon iconfont icon-kefuyouxian'></i>
                <div>会员</div>
            </li>
            <li>
                <i class='icon iconfont icon-31shezhi'></i>
                <div>设置</div>
            </li>
        </ul>
    </div>
</template>
<script>
export default {
    
}
</script>
<style scoped>
.left-nav{
    color:white;
    font-size: 10px;
    height: 100%;
    background-color: #1d8ce0;
    float:left;
    width: 5%;
}
.iconfont{
    font-size: 24px;
}
.left-nav ul{
    padding: 0px;
    margin: 0px;
}
.left-nav li{
    list-style: none;
    text-align: center;
    border-bottom: 1px solid rgb(211, 192, 192);
    padding: 10px;
}
</style>
