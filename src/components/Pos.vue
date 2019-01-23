<template>
  <div class="pos">
    <div>
      <el-row>
        <el-col :span="7" class="oder-list" id="order-list">
          <el-tabs>
            <el-tab-pane label="点餐">
              <!-- 商品显示表格 -->
              <el-table v-bind:data="tableData" border>
                <el-table-column prop="goodsName" label="商品名称"></el-table-column>
                <el-table-column prop="count" label="数量"></el-table-column>
                <el-table-column prop="price" label="价格"></el-table-column>
                <!-- 将操作栏固定在右边 -->
                <el-table-column label="操作" width="100" fixed="right">
                  <template slot-scope="scope">
                    <el-button
                      type="text"
                      size="small"
                      @click="headleDelete(scope.$index, scope.row)"
                    >删除</el-button>
                    <!-- 注意：这里没有goods，要将整行的数据都传进去 -->
                    <el-button
                      type="text"
                      size="small"
                      @click="headleAdd(scope.$index, scope.row)"
                    >增加</el-button>
                  </template>
                </el-table-column>
              </el-table>
              <!-- 合计数量 和 价格 -->
              <div class="totalDiv">
                <small>数量</small>
                {{totalCount}}个
                <small>价格</small>
                {{totalPrice}}元
              </div>
              <!-- 挂单 删除 结账 按钮 -->
              <div class="div-btn">
                <el-button type="warning" @click='sendOut'>挂单</el-button>
                <el-button type="danger" @click="checkout">结账</el-button>
                <el-button type="success" @click='deleteAllGoods'>删除</el-button>
              </div>
            </el-tab-pane>
            <el-tab-pane label="挂单">挂单</el-tab-pane>
            <el-tab-pane label="外卖">外卖</el-tab-pane>
          </el-tabs>
        </el-col>
        <!--商品展示-->
        <el-col :span="17">
          <!-- 商品列表 -->
          <h3 class="goodsTitle">商品列表</h3>
          <!-- 热卖商品 -->
          <div class="hotGoods">
            <ul>
              <li v-for="(item,index) in oftenGoods" :key="index" @click="addTableData(item)">
                <span class="offenGoodsName">{{ item.goodsName }}</span>
                <span class="offenGoodsPrice">${{ item.price }}</span>
              </li>
            </ul>
          </div>
          <!-- 商品展示 -->
          <div class="goodsList">
            <!-- 商品tab栏 -->
            <el-tabs>
              <el-tab-pane label="汉堡">
                <div class="goodsList">
                  <ul>
                    <li v-for="(item, index) in hanbao" @click="addTableData(item)" :key="index">
                      <span>
                        <img :src="item.goodsImg">
                      </span>
                      <span>{{item.goodsName}}</span>
                      <span>${{item.price}}</span>
                    </li>
                  </ul>
                </div>
              </el-tab-pane>
              <el-tab-pane label="小吃">
                <div class="goodsList">
                  <ul>
                    <li v-for="(item,index) in xiaochi" @click="addTableData(item)" :key="index">
                      <span>
                        <img :src="item.goodsImg">
                      </span>
                      <span>{{item.goodsName}}</span>
                      <span>${{item.price}}</span>
                    </li>
                  </ul>
                </div>
              </el-tab-pane>
              <el-tab-pane label="饮料">
                <div class="goodsList">
                  <ul>
                    <li v-for="(item, index) in yinliao" @click="addTableData(item)" :key="index">
                      <span>
                        <img :src="item.goodsImg">
                      </span>
                      <span>{{item.goodsName}}</span>
                      <span>${{item.price}}</span>
                    </li>
                  </ul>
                </div>
              </el-tab-pane>
              <el-tab-pane label="甜点">
                  <div class="goodsList">
                  <ul>
                    <li v-for="(item,index) in tiandian" @click="addTableData(item)" :key="index">
                      <span>
                        <img :src="item.goodsImg">
                      </span>
                      <span>{{item.goodsName}}</span>
                      <span>${{item.price}}</span>
                    </li>
                  </ul>
                </div>
              </el-tab-pane>
            </el-tabs>
          </div>
        </el-col>
      </el-row>
    </div>
  </div>
</template>

<script>
export default {
  name: "Pos",
  data() {
    return {
      tableData: [],
      oftenGoods: [
        {
          goodsId: 1,
          goodsName: "香辣鸡腿堡",
          price: 12
        },
        {
          goodsId: 2,
          goodsName: "田园鸡腿堡",
          price: 15
        },
        {
          goodsId: 18,
          goodsName: "和风汉堡",
          price: 15
        },
        {
          goodsId: 4,
          goodsName: "快乐全家桶",
          price: 80
        },
        {
          goodsId: 19,
          goodsName: "脆皮炸鸡腿",
          price: 10
        },
        {
          goodsId: 20,
          goodsName: "魔法鸡块",
          price: 20
        },
        {
          goodsId: 21,
          goodsName: "可乐大杯",
          price: 10
        },
        {
          goodsId: 22,
          goodsName: "雪顶咖啡",
          price: 18
        },
        {
          goodsId: 23,
          goodsName: "大块鸡米花",
          price: 15
        },
        {
          goodsId: 24,
          goodsName: "香脆鸡柳",
          price: 17
        },
        {
          goodsId: 25,
          goodsName: "小份薯条",
          price: 12
        },
        {
          goodsId: 12,
          goodsName: "红豆派",
          price: 8
        }
      ],
      hanbao: [],
      xiaochi: [],
      yinliao: [],
      tiandian: [],
      totalPrice: 0,
      totalCount: 0
    }
  },
  methods: {
    
    // 点击商品添加都商品栏当中
    addTableData (goods) { 
        // 判断该商品在不在当前商品栏中
        let isHave = false;
        for (var i = 0; i < this.tableData.length; i++) {
            if (this.tableData[i].goodsId === goods.goodsId) {
                isHave = true;
            }
        }

        if (isHave) { // 如果在商品列表中，只要更改数量就可以了
            // 将点击的商品从列表中筛选出来
            let arr = this.tableData.filter(o => o.goodsId == goods.goodsId)
            arr[0].count++;
        } else { // 如果不在商品列表当中，将商品追加到商品数组中
            let newGoods = {
                goodsId: goods.goodsId,
                goodsName: goods.goodsName,
                price: goods.price,
                count: 1
            };

            this.tableData.push(newGoods);
        }

        this.countAllPrice();

    },

    // 计算总的数量 和 价格
    countAllPrice() {
      this.totalPrice = 0;
      this.totalCount = 0;
      // 循环遍历 tableData 数组，进行计算
      for (let value of this.tableData.values()) {
        // console.log(value)
        this.totalPrice += value.price * value.count;
        this.totalCount += value.count;
      }

    },

    // 删除单个商品
    headleDelete(index, row) {
      // console.log(index, row);
      // console.log(row.count);
      this.tableData = this.tableData.filter(o => row.goodsId != o.goodsId);
      // 重新计算总的价格
      this.countAllPrice();
    },
    // 增加单个商品
    headleAdd(index, row) {
      // console.log(index, row);
      // 将当前元素的count加1，在计算一遍总数量 和 金额
      let newArr = this.tableData.filter(o => row.goodsId == o.goodsId);
      newArr[0].count++;

      this.countAllPrice();
    },
    // 删除全部商品
    deleteAllGoods () {
      this.totalPrice = 0;
      this.totalCount = 0;
      this.tableData = [];
    },

    // 结账
    checkout () {
      // 判断总金额是否为 0
      if (this.totalPrice == 0 && this.totalCount == 0) {
        this.$message({
          type: 'info',
          message: '请选择商品'
        })
      } else {
        this.$message({
          type: 'success',
          message: `结账成功,总共消费${this.totalPrice}元`
        });
      }

      // 结完张后，清空列表
      this.deleteAllGoods();

    },

    // 挂单
    sendOut () {
      this.$message({
        type:'warning',
        message: `挂单成功`
      })
    }
  },
  mounted: function() {
    // 当页面加载完时执行
    let orderHeight = document.body.clientHeight;
    // console.log(orderHeight);
    document.getElementById("order-list").style.height = orderHeight + "px";
  },
  created: function() {
    this.$axios.get("http://localhost:3000/hanbao").then(response => {
      this.hanbao = response.data;
    //   console.log(this.hanbao[0].goodsImg);
    });
    this.$axios.get("http://localhost:3000/xiaochi").then(response => {
      this.xiaochi = response.data;
    //   console.log(this.xiaochi);
    });
    this.$axios.get("http://localhost:3000/yinliao").then(response => {
      this.yinliao = response.data;
    //   console.log(this.yinliao);
    });
    this.$axios.get("http://localhost:3000/tiandian").then(response => {
      // console.log(response.data);
      this.tiandian = response.data;
    //   console.log(this.tiandian);
    });

    // 使用axios来同时获取多个数据
  //   var obj = {
  //     hanbao: this.$axios.get("http://localhost:3000/hanbao"),
  //     xiaochi: this.$axios.get("http://localhost:3000/xiaochi"),
  //     yinliao: this.$axios.get("http://localhost:3000/yinliao"),
  //     tiandian: this.$$axios.get("http://localhost:3000/tiandian"),
  //   };

  //   this.$axios.all([obj.hanbao, obj.xiaochi, obj.yinliao, obj.tiandian])
  //              .then(this.$axios.spread((hanbao, xiaochi, yinliao, tiandian) => {
  //                this.hanbao = hanbao.data;
  //                this.xiaochi = xiaochi.data;
  //                this.yinliao = yinliao.data;
  //                this.tiandian = tiandian.data;
  //              }))

  }
}
</script>

<style scoped>
.pos {
  width: 95%;
  height: 100%;
  float: right;
}
.oder-list {
  background-color: #fff;
  border-right: 1px solid #1d8ce0;
  height: 100%;
}
.pro-list {
  height: 100%;
  float: right;
}
.tab_diancan {
  padding-left: 20px;
}
.totalDiv {
  width: 100%;
  height: 50px;
  line-height: 50px;
  background: skyblue;
}
.totalDiv > small {
  font-size: 20px;
  color: #000;
}
.div-btn {
  margin-top: 20px;
}
.goodsTitle {
  color: #666;
  margin-bottom: 10px;
}
.hotGoods {
  width: 100%;
  height: 300px;
  padding: 20px;
  border-top: 1px solid #ccc;
  box-sizing: border-box;
  /* background: #ccc; */
}
.hotGoods > ul {
  width: 100%;
  height: 100%;
  clear: both;
}
.hotGoods > ul > li {
  list-style: none;
  float: left;
  margin-right: 20px;
  margin-top: 30px;
  width: 120px;
  height: 50px;
  cursor: pointer;
  background: skyblue;
}
.hotGoods > ul > li > span:first-of-type {
  color: #fff;
  font-size: 20px;
}
.hotGoods > ul > li > span:last-of-type {
  display: block;
  margin-top: 5px;
  color: red;
}

/* 商品展示 */
.goodsList {
  width: 100%;
  height: 500px;
  /* background: pink; */
}
.goodsList > ul {
  width: 100%;
  height: 100%;
  list-style: none;
  clear: both;
  box-sizing: border-box;
}
.goodsList > ul > li {
  width: 200px;
  height: 200px;
  margin-right: 30px;
  margin-bottom: 30px;
  background: skyblue;
  float: left;
  cursor: pointer;
  box-shadow: 1px 5px 20px #ccc;
}
.goodsList > ul > li > span:nth-child(1) {
  width: 100px;
  height: 100px;
}
.goodsList > ul > li > span:nth-child(1) > img {
  width: 100px;
  height: 100px;
  display: block;
  margin: 0 50px;
  margin-top: 10px;
}
.goodsList > ul > li > span:nth-child(2) {
  margin-top: 10px;
  display: block;
  color: #fff;
}
.goodsList > ul > li > span:nth-child(3) {
  margin-top: 10px;
  display: block;
  color: red;
}
</style>

