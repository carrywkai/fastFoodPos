<template>
    <ul>
        <li>
            <a href="javascript:;">
                <i class="icon iconfont icon-tubiao-"></i>
                <div>收银</div>
            </a>
        </li>
         <li>
            <a href="javascript:;">
                <i class="icon iconfont icon-dianpu"></i>
                <div>店铺</div>
            </a>
        </li>
         <li>
            <a href="javascript:;">
                <i class="icon iconfont icon-shouye"></i>
                <div>商品</div>
            </a>
        </li>
         <li>
            <a href="javascript:;">
                <i class="icon iconfont icon-wode"></i>
                <div>会员</div>
            </a>
        </li>
         <li>
            <a href="javascript:;">
                <i class="icon iconfont icon-erweima"></i>
                <div>统计</div>
            </a>
        </li>
    </ul>
</template>

<script>
export default {
    name: 'leftNav'
}
</script>

<style scoped>
    ul {
        list-style: none;
        width: 5%;
        height: 100%;
        float: left;
        margin: 0;
        padding: 0;
        background: #1D8ce0;
    }
    ul > li{
        width: 100%;
        height: 100px;
        border-bottom: 1px solid #fff;
    }
    ul > li > a{
        width: 100%;
        height: 100%;
        display: block;
        text-decoration: none;
    }

    ul > li > a > i{
        font-size: 50px;
        margin-top: 10px;
        display: inline-block;
        color: #fff;
    }
    ul > li > a > div{
        font-size: 20px;
        color: #fff;
    }

</style>


