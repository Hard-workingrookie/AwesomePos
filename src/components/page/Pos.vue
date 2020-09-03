<template>
  <div class="pos">
    <div>
      <el-row>
        <el-col :span="7" id="order-list" class="pos-order">
          <el-tabs>
            <el-tab-pane label="点餐">
              <el-table :data="tableData" border show-summary style="width: 100%">
                <el-table-column prop="goodsName" label="商品"></el-table-column>
                <el-table-column prop="count" label="量" width="50"></el-table-column>
                <el-table-column prop="price" label="金额" width="70"></el-table-column>
                <el-table-column label="操作" width="100" fixed="right">
                  <template scope="scope">
                    <el-button type="text" size="small" @click="delSingleGoods(scope.row)">删除</el-button>
                    <el-button type="text" size="small" @click="addOrderList(scope.row)">增加</el-button>
                  </template>
                </el-table-column>
              </el-table>
              <div class="totalDiv">
                <small>数量:</small>
                {{totalCount}} &nbsp;&nbsp;&nbsp;
                <small>数量:</small>
                {{totalMoney}}元
              </div>
              <el-button class="pos-order-btn" type="warning">挂单</el-button>
              <el-button class="pos-order-btn" type="danger" @click="delAllGoods()">删除</el-button>
              <el-button class="pos-order-btn" type="success" @click="checkout()">结账</el-button>
            </el-tab-pane>
            <el-tab-pane label="挂单">挂单</el-tab-pane>
            <el-tab-pane label="外卖">外卖</el-tab-pane>
          </el-tabs>
        </el-col>
        <!--商品展示-->
        <el-col :span="17" class="pos-product">
          <div class="often-goods">
            <div class="title">常用商品</div>
            <div class="often-goods-list">
              <ul>
                <li v-for="good in oftenGoods" @click="addOrderList(good)">
                  <span>{{good.goodsName}}</span>
                  <span class="o-price">￥{{good.price}}元</span>
                </li>
              </ul>
            </div>
          </div>
          <div class="goods-type">
            <el-tabs>
              <el-tab-pane label="汉堡">
                <ul class="cookList">
                  <li v-for="good in type0Goods" @click="addOrderList(good)">
                    <span class="foodImg">
                      <img width="100%" :src="good.goodsImg" />
                    </span>
                    <span class="foodName">{{good.goodsName}}</span>
                    <span class="foodPrice">￥{{good.price}}元</span>
                  </li>
                </ul>
              </el-tab-pane>
              <el-tab-pane label="小食">
                <ul class="cookList">
                  <li v-for="good in type1Goods" @click="addOrderList(good)">
                    <span class="foodImg">
                      <img width="100%" :src="good.goodsImg" />
                    </span>
                    <span class="foodName">{{good.goodsName}}</span>
                    <span class="foodPrice">￥{{good.price}}元</span>
                  </li>
                </ul>
              </el-tab-pane>
              <el-tab-pane label="饮料">
                <ul class="cookList">
                  <li v-for="good in type2Goods" @click="addOrderList(good)">
                    <span class="foodImg">
                      <img width="100%" :src="good.goodsImg" />
                    </span>
                    <span class="foodName">{{good.goodsName}}</span>
                    <span class="foodPrice">￥{{good.price}}元</span>
                  </li>
                </ul>
              </el-tab-pane>
              <el-tab-pane label="套餐">
                <ul class="cookList">
                  <li v-for="good in type3Goods" @click="addOrderList(good)">
                    <span class="foodImg">
                      <img width="100%" :src="good.goodsImg" />
                    </span>
                    <span class="foodName">{{good.goodsName}}</span>
                    <span class="foodPrice">￥{{good.price}}元</span>
                  </li>
                </ul>
              </el-tab-pane>
            </el-tabs>
          </div>
        </el-col>
      </el-row>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Pos",
  mounted: function () {
    var orderHeight = document.body.clientHeight;
    document.getElementById("order-list").style.height = orderHeight + "px";
  },
  created() {
    axios
      .get(
        "https://www.easy-mock.com/mock/5b8b30dbf032f03c5e71de7f/kuaican/oftenGoods"
      )
      .then((response) => {
        console.log("hhhhhhhhhhhhh", response);
        this.oftenGoods = response.data;
      })
      .catch((error) => {
        console.log(error);
        // alert('网络错误，不能访问');
      });
    //读取分类商品列表
    axios
      .get(
        "https://www.easy-mock.com/mock/5b8b30dbf032f03c5e71de7f/kuaican/typeGoods"
      )
      .then((response) => {
        console.log(response);
        // this.oftenGoods=response.data;
        this.type0Goods = response.data[0];
        this.type1Goods = response.data[1];
        this.type2Goods = response.data[2];
        this.type3Goods = response.data[3];
      })
      .catch((error) => {
        console.log(error);
        alert("网络错误，不能访问");
      });
  },
  data() {
    return {
      tableData: [],
      oftenGoods: [],
      type0Goods: [
        // {
        //   goodsId: 1,
        //   goodsImg:
        //     "http://officialwebsitestorage.blob.core.chinacloudapi.cn/public/upload/attachment/2020/03/202003191444328139.png",
        //   goodsName: "香辣鸡腿堡",
        //   price: 18,
        // },
        // {
        //   goodsId: 2,
        //   goodsImg:
        //     "http://officialwebsitestorage.blob.core.chinacloudapi.cn/public/upload/attachment/2020/03/202003191446371767.png",
        //   goodsName: "田园鸡腿堡",
        //   price: 15,
        // },
        // {
        //   goodsId: 3,
        //   goodsImg:
        //     "http://officialwebsitestorage.blob.core.chinacloudapi.cn/public/upload/attachment/2020/03/202003191431284513.png",
        //   goodsName: "和风汉堡",
        //   price: 15,
        // },
        // {
        //   goodsId: 4,
        //   goodsImg:
        //     "http://officialwebsitestorage.blob.core.chinacloudapi.cn/public/upload/attachment/2020/04/202004291713404547.png",
        //   goodsName: "快乐全家桶",
        //   price: 80,
        // },
        // {
        //   goodsId: 5,
        //   goodsImg:
        //     "http://officialwebsitestorage.blob.core.chinacloudapi.cn/public/upload/attachment/2020/05/202005061003553790.png",
        //   goodsName: "脆皮炸鸡腿",
        //   price: 10,
        // },
        // {
        //   goodsId: 6,
        //   goodsImg:
        //     "http://officialwebsitestorage.blob.core.chinacloudapi.cn/public/upload/attachment/2020/03/202003191446258631.png",
        //   goodsName: "魔法鸡块",
        //   price: 20,
        // },
        // {
        //   goodsId: 7,
        //   goodsImg:
        //     "http://officialwebsitestorage.blob.core.chinacloudapi.cn/public/upload/attachment/2020/03/202003191431284513.png",
        //   goodsName: "可乐大杯",
        //   price: 10,
        // },
        // {
        //   goodsId: 8,
        //   goodsImg:
        //     "http://officialwebsitestorage.blob.core.chinacloudapi.cn/public/upload/attachment/2020/05/202005270940031690.png",
        //   goodsName: "雪顶咖啡",
        //   price: 18,
        // },
        // {
        //   goodsId: 9,
        //   goodsImg:
        //     "http://officialwebsitestorage.blob.core.chinacloudapi.cn/public/upload/attachment/2015/11/201511061707075050.png",
        //   goodsName: "大块鸡米花",
        //   price: 15,
        // },
        // {
        //   goodsId: 20,
        //   goodsImg:
        //     "http://officialwebsitestorage.blob.core.chinacloudapi.cn/public/upload/attachment/2020/03/202003191446258631.png",
        //   goodsName: "香脆鸡柳",
        //   price: 17,
        // },
      ],
      type1Goods: [],
      type2Goods: [],
      type3Goods: [],
      totalMoney: 0,
      totalCount: 0,
    };
  },
  methods: {
    // 添加订单列表的方法
    addOrderList(goods) {
      this.totalCount = 0; // 汇总数量清0
      this.totalMoney = 0;
      let isHave = false;
      // 判断是否这个商品已经存在于订单列表
      for (let i = 0; i < this.tableData.length; i++) {
        console.log(this.tableData[i].goodsId);
        if (this.tableData[i].goodsId == goods.goodsId) {
          isHave = true; // 存在
        }
      }
      // 根据isHave的值判断订单列表中是否已经有此商品
      if (isHave) {
        // 存在就进行数量添加
        let arr = this.tableData.filter((o) => o.goodsId == goods.goodsId);
        arr[0].count++;
        //console.log(arr);
      } else {
        // 不存在就推入数组
        let newGoods = {
          goodsId: goods.goodsId,
          goodsName: goods.goodsName,
          price: goods.price,
          count: 1,
        };
        this.tableData.push(newGoods);
      }

      // 进行数量和价格的汇总计算
      this.tableData.forEach((element) => {
        this.totalCount += element.count;
        this.totalMoney = this.totalMoney + element.price * element.count;
      });
    },
    // 删除单个商品
    delSingleGoods(goods) {
      // console.log(goods);
      this.tableData = this.tableData.filter((o) => o.goodsId != goods.goodsId);
      this.getAllMoney();
    },

    //汇总数量和金额
    getAllMoney() {
      this.totalCount = 0;
      this.totalMoney = 0;
      if (this.tableData) {
        this.tableData.forEach((element) => {
          this.totalCount += element.count;
          this.totalMoney = this.totalMoney + element.price * element.count;
        });
      }
    },
    delAllGoods() {
      this.$confirm("此操作将删除所有加购商品, 是否继续?", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        type: "warning",
      })
        .then(() => {
          this.$message({
            type: "success",
            message: "删除成功!",
          });
          this.tableData = [];
          this.totalCount = 0;
          this.totalMoney = 0;
        })
        .catch(() => {
          this.$message({
            type: "info",
            message: "已取消删除",
          });
        });
    },
    checkout() {
      if (this.totalCount != 0) {
        this.tableData = [];
        this.totalCount = 0;
        this.totalMoney = 0;
        this.$message({
          message: "结账成功，感谢你又为店里出了一份力!",
          type: "success",
        });
      } else {
        this.$message.error("不能空结。老板了解你急切的心情！");
      }
    },
  },
};
</script>
<style scoped>
/* 左边 */
.pos-order {
  background-color: #eee;
  padding: 20px;
  border-right: 1px solid #ccc;
}
.pos-product {
  padding: 20px;
}
.pos-order-btn {
  margin: 10px;
  float: right;
}
.totalDiv {
  background-color: #fff;
  padding: 10px;
  border-bottom: 1px solid #ccc;
}

/* 右边 */

.title {
  height: 20px;
  border-bottom: 1px solid #d3dce6;
  background-color: #f9fafc;
  padding: 10px;
}
.often-goods-list ul li {
  list-style: none;
  float: left;
  border: 1px solid #e5e9f2;
  padding: 10px;
  margin: 5px;
  background-color: #fff;
  border-radius: 2px;
  cursor: pointer;
}
.o-price {
  color: #58b7ff;
}

.goods-type {
  clear: both;
}
.cookList li {
  list-style: none;
  width: 200px;
  border: 1px solid #e5e9f2;
  height: 100px;
  overflow: hidden;
  background-color: #fff;
  padding: 2px;
  float: left;
  margin: 10px;
  cursor: pointer;
}
.cookList li span {
  display: block;
  float: left;
}
.foodImg {
  width: 40%;
  height: 100%;
}
.foodName {
  font-size: 18px;
  padding-left: 10px;
  color: brown;
  margin-top: 10px;
}
.foodPrice {
  font-size: 16px;
  padding-left: 10px;
  margin-top: 10px;
}
</style>