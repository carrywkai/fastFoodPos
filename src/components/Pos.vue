<template>
    <div class="pos">
        <div>
            <el-row>
                <el-col :span='7' class="oder-list" id="order-list">
                    标签栏
                </el-col>
                <!--商品展示-->
                <el-col :span='17'>
                    商品展示
                </el-col>
            </el-row>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Pos',
    mounted: function () { // 当页面加载完时执行
        let orderHeight = document.body.clientHeight;
        console.log(orderHeight);
        document.getElementById('order-list').style.height = orderHeight + 'px';
    }
}
</script>

<style scoped>
    .pos{
        width: 95%;
        height: 100%;
        float: right;
    }
    .oder-list{
        background-color: #ccc;
        border-right: 1px solid #1D8ce0;
    }
    .pro-list{
        height: 100%;
        float: right;
    }
</style>

