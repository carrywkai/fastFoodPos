<template>
    <div class="pos">
        <div>
            <el-row>
                <el-col :span='7' class="oder-list" id="order-list">
                    <el-tabs>
                        <el-tab-pane label='点餐'>
                            <!-- 商品显示表格 -->
                            <el-table v-bind:data="tableData" border>
                                <el-table-column prop='goodsName' label='商品名称'></el-table-column>
                                <el-table-column prop='count' label='数量'></el-table-column>
                                <el-table-column prop='price' label='价格'></el-table-column>
                                <!-- 将操作栏固定在右边 -->
                                <el-table-column label='操作' width='100' fixed='right'>
                                         <template slot-scope="scope">
                                             <el-button type="text" size="small" @click='headleDelete(scope.$index, scope.row)'>删除</el-button>
                                             <!-- 注意：这里没有goods，要将整行的数据都传进去 -->
                                             <el-button type="text" size="small" @click='headleAdd(scope.$index, scope.row)'>增加</el-button>
                                         </template>
                                </el-table-column>
                            </el-table>
                            <!-- 合计数量 和 价格 -->
                            <div class="totalDiv">
                                <small>数量</small>
                                0个
                                <small>价格</small>
                                0元
                            </div>
                            <!-- 挂单 删除 结账 按钮 -->
                            <div class="div-btn">
                                <el-button type='warning'>挂单</el-button>
                                <el-button type='danger'>结账</el-button>
                                <el-button type='success'>删除</el-button>
                            </div>
                        </el-tab-pane>
                        <el-tab-pane label='挂单'>
                            挂单
                        </el-tab-pane>
                        <el-tab-pane label='外卖'>
                            外卖
                        </el-tab-pane>
                    </el-tabs>
                </el-col>
                <!--商品展示-->
                <el-col :span='17'>
                    <!-- 商品列表 -->
                    <h3 class="goodsTitle">商品列表</h3>
                    <!-- 热卖商品 -->
                    <div class="hotGoods">
                        <ul>
                            <li v-for="goods in oftenGoods" :key="goods.goodsId">
                                <span class="offenGoodsName">{{ goods.goodsName }}</span>
                                <span class="offenGoodsPrice">${{ goods.price }}</span>
                            </li>
                        </ul>
                    </div>
                    <!-- 商品展示 -->
                    <div class="goodsList">
                        <!-- 商品tab栏 -->
                        <el-tabs>
                            <el-tab-pane label='汉堡'>
                                <div class="goodsList">
                                    <ul>
                                        <li>
                                            <span>
                                                <img src="../assets/images/logo.png" alt="">
                                            </span>
                                            <span>香辣鸡腿堡</span>
                                            <span>$20.00</span>
                                        </li>
                                    </ul>
                                </div>
                            </el-tab-pane>
                            <el-tab-pane label='小吃'>小吃</el-tab-pane>
                            <el-tab-pane label='饮料'>饮料</el-tab-pane>
                            <el-tab-pane label='甜点'>甜点</el-tab-pane>
                        </el-tabs>
                    </div>
                </el-col>
            </el-row>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Pos',
    data () {
        return {
            tableData: [
                 {
                   goodsName: '可口可乐',
                   price: 8,
                   count:1
                 }, 
                 {
                   goodsName: '香辣鸡腿堡',
                   price: 15,
                   count:1
                 },
                  {
                   goodsName: '爱心薯条',
                   price: 8,
                   count:1
                 }, 
                 {
                   goodsName: '甜筒',
                   price: 8,
                   count:1
                 },
                 {
                   goodsName: '薯条',
                   price: 8,
                   count:1
                 },
                 {
                   goodsName: '派',
                   price: 12,
                   count:1
                 }
            ],
            oftenGoods:[
                {
                    goodsId:1,
                    goodsName:'香辣鸡腿堡',
                    price:18
                },
                {
                    goodsId:2,
                    goodsName:'田园鸡腿堡',
                    price:15
                },
                {
                    goodsId:3,
                    goodsName:'和风汉堡',
                    price:15
                },
                {
                    goodsId:4,
                    goodsName:'快乐全家桶',
                    price:80
                },
                {
                    goodsId:5,
                    goodsName:'脆皮炸鸡腿',
                    price:10
                },
                {
                    goodsId:6,
                    goodsName:'魔法鸡块',
                    price:20
                },
                {
                    goodsId:7,
                    goodsName:'可乐大杯',
                    price:10
                },
                {
                    goodsId:8,
                    goodsName:'雪顶咖啡',
                    price:18
                },
                {
                    goodsId:9,
                    goodsName:'大块鸡米花',
                    price:15
                },
                {
                    goodsId:20,
                    goodsName:'香脆鸡柳',
                    price:17
                },
                {
                    goodsId:21,
                    goodsName:'小份薯条',
                    price:12
                },
                 {
                    goodsId:22,
                    goodsName:'派',
                    price:10
                }
            ],
            type0Goods:[
                    {
                        goodsId:1,
                        goodsImg:"../assets/images/logo.png",
                        goodsName:'香辣鸡腿堡',
                        price:18
                    }, 
                    {
                        goodsId:2,
                        goodsImg:"../assets/images/logo.png",
                        goodsName:'田园鸡腿堡',
                        price:15
                    }, 
                    {
                        goodsId:3,
                        goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
                        goodsName:'和风汉堡',
                        price:15
                    }, 
                    {
                        goodsId:4,
                         goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
                        goodsName:'快乐全家桶',
                        price:80
                    }, 
                    {
                        goodsId:5,
                         goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
                        goodsName:'脆皮炸鸡腿',
                        price:10
                    }, 
                    {
                        goodsId:6,
                         goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
                        goodsName:'魔法鸡块',
                        price:20
                    }, 
                    {
                        goodsId:7,
                         goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
                        goodsName:'可乐大杯',
                        price:10
                    }, 
                    {
                        goodsId:8,
                         goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
                        goodsName:'雪顶咖啡',
                        price:18
                    }, 
                    {
                        goodsId:9,
                         goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
                        goodsName:'大块鸡米花',
                        price:15
                    }, 
                    {
                        goodsId:20,
                         goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
                        goodsName:'香脆鸡柳',
                        price:17
                    }
            ],    

        }
    },
    medthods: {
        headleDelete (index,row) {
            console.log(index, row);
        },
        headleAdd (index,row) {
            console.log(index, row);
        }
    },
    mounted: function () { // 当页面加载完时执行
        let orderHeight = document.body.clientHeight;
        // console.log(orderHeight);
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
        background-color: #fff;
        border-right: 1px solid #1D8ce0;
        height: 100%;
    }
    .pro-list{
        height: 100%;
        float: right;
    }
    .tab_diancan{
        padding-left: 20px;
    }
    .totalDiv{
        width: 100%;
        height: 50px;
        line-height: 50px;
        background: skyblue;
    }
    .totalDiv > small {
        font-size: 20px;
        color: #000;
    }
    .div-btn{
        margin-top: 20px;
    }
    .goodsTitle{
        color: #666;
        margin-bottom: 10px;
    }
    .hotGoods{
        width: 100%;
        height: 300px;
        padding: 20px;
        border-top: 1px solid #ccc;
        box-sizing: border-box;
        /* background: #ccc; */
    }
    .hotGoods > ul{
        width: 100%;
        height: 100%;
        clear: both;
    }
    .hotGoods > ul > li{
        list-style: none;
        float: left;
        margin-right: 20px;
        margin-top: 30px;
        width: 120px;
        height: 50px;
        cursor: pointer;
        background: skyblue;
    }
    .hotGoods > ul > li > span:first-of-type{
        color: #fff;
        font-size: 20px;
    }
    .hotGoods > ul > li > span:last-of-type{
        display: block;
        margin-top: 5px;
        color: red;
    }

    /* 商品展示 */
    .goodsList{
        width: 100%;
        height: 500px;
        /* background: pink; */
    }
    .goodsList > ul{
        width: 100%;
        height: 100%;
        list-style: none;
        clear: both;
        box-sizing: border-box;
    }
    .goodsList > ul > li{
        width: 200px;
        height: 200px;
        margin-right: 30px;
        margin-bottom: 30px;
        background: skyblue;
        cursor: pointer;
        box-shadow: 1px 5px 20px #ccc;
        
    }
    .goodsList > ul > li > span:nth-child(1){
        width: 100px;
        height: 100px;
    }
    .goodsList > ul > li > span:nth-child(1) > img{
        width: 100px;
        height: 100px;
        display: block;
        margin: 0 50px;
    }
    .goodsList > ul > li > span:nth-child(2){
        margin-top: 10px;
        display: block;
        color: #fff;
    }
    .goodsList > ul > li > span:nth-child(3){
        margin-top: 10px;
        display: block;
        color: red;
    }
</style>

