<template>
    <div class="">
        <div class="container">
            <el-tabs v-model="activeName">
            
                <el-tab-pane :label="`新增加或修改商品`" name="first"> 
                   
                   <template>

        <div class="container" v-loading="querying"
    element-loading-text="执行中"
    element-loading-spinner="el-icon-loading"
    element-loading-background="rgba(0, 0, 0, 0.8)">
            <input id="file" class="file" style="display:none" name="file" type="file" accept="image/png,image/gif,image/jpeg" @change="update"/>
 <img :src="imgUrl">
 <el-button type="primary" @click="chooseImg">图片选择</el-button>
            <br/>
            <br/>
             <el-select v-model="classid" class="cselect">
          <el-option v-for="item in types" :key="item.classid" :label="item.classname" :value="item.classid">
          </el-option>
        </el-select>
        <el-input style="width:100px" v-model="sort_id" placeholder="排序id"></el-input>
         
        <br/>
         <br/>
             <el-input v-model="name" placeholder="商品名"></el-input>
             <br/>
         <br/>
             <el-input style="width:100px" v-model="price" placeholder="价格"></el-input>
             <el-input class="cinput" v-model="price_desc" placeholder="价格描述"></el-input>
         <br/>
         <br/>
             <el-input style="width:100px" v-model="rush_price" placeholder="闯关价"></el-input>
             <el-input class="cinput" v-model="rush_price_desc" placeholder="闯关价描述"></el-input>
              <br/>
         <br/>
             <el-input style="width:300px" v-model="goods_desc" placeholder="色号"></el-input>
             <el-input style="width:300px" v-model="brand" placeholder="品牌名"></el-input>
                <br/>
         <br/>
          <el-input style="width:150px" v-model="level[0].count" placeholder="第一关口红数"></el-input>
          <el-input style="width:150px" v-model="level[0].time" placeholder="游戏时间(秒)"></el-input>
          <el-input style="width:150px" v-model="level[0].difficulty" placeholder="难度系数[1-100]"></el-input>
           <br/>
           <br/>
            <el-input style="width:150px" v-model="level[1].count" placeholder="第二关口红数"></el-input>
          <el-input style="width:150px" v-model="level[1].time" placeholder="游戏时间(秒)"></el-input>
          <el-input style="width:150px" v-model="level[1].difficulty" placeholder="难度系数[1-100]"></el-input>
           <br/>
           <br/>
            <el-input style="width:150px" v-model="level[2].count" placeholder="第三关口红数"></el-input>
          <el-input style="width:150px" v-model="level[2].time" placeholder="游戏时间(秒)"></el-input>
          <el-input style="width:150px" v-model="level[2].difficulty" placeholder="难度系数[1-100]"></el-input>
           <br/>
           <br/>
              <el-button type="success" @click="commit">提交</el-button>
    </div>
</template>
                </el-tab-pane>
                <el-tab-pane :label="`商品查询`" name="second">
                 <!-- <el-table
    :data="tableData"
    :cell-style="cellClass"
    @selection-change="handleSelectionChange"
    border>
    <el-table-column
      type="selection"
      width="50">
    </el-table-column>
    <el-table-column
      label="商品id"
      width="50"
      align="center">
      <template slot-scope="scope">
       <p>{{scope.row.id}}</p>
      </template>
    </el-table-column>
    <el-table-column
        label="商品图片"
        width="100"
        align="center">
      <template slot-scope="scope">
      <img :src= "scope.row.min">
  <el-input  v-model="scope.row.min"  ></el-input>
      </template>
    </el-table-column>
    <el-table-column
      label="商品名称"
      width="90"
      align="center">
      <template slot-scope="scope">
       <el-input :id="tableInputId+scope.$index" @keyup.enter.native="enterNext(0, scope.$index)" v-model="scope.row.tableId" placeholder="桌号" v-on:change="isAddRow(scope.$index)"></el-input>
      </template>
    </el-table-column>
    <el-table-column
      label="商品价格描述"
      width="110"
      align="center">
      <template slot-scope="scope">
        <el-select v-model="scope.row.leagueId" :id="leagueInputId+scope.$index" @keyup.enter.native="enterNext(1, scope.$index)">
          <el-option v-for="item in scope.row.types" :key="item.Id" :label="item.Name" :value="item.Id">
          </el-option>
        </el-select>
      </template>
    </el-table-column>
    <el-table-column
      label="游戏ID"
      width="140"
      align="center">
      <template slot-scope="scope">
       <el-input :id="gidInputId+scope.$index" @keyup.enter.native="enterNext(2, scope.$index)" v-model="scope.row.gid" placeholder="游戏ID" v-on:change="getTR(scope.$index)"></el-input>
      </template>
    </el-table-column>
    <el-table-column
        prop="tid"
        label="玩家账号"
        width="140"
        align="center">
    </el-table-column>
    <el-table-column
      label="带入积分"
      width="90"
      align="center">
      <template slot-scope="scope">
       <el-input :id="scoreInputId+scope.$index" @keyup.enter.native="enterNext(3, scope.$index)" v-model="scope.row.score" placeholder="积分" v-on:change="computeTotal(scope.$index,false)"></el-input>
      </template>
    </el-table-column>
    <el-table-column
      label="会员积分"
      width="100"
      align="center">
      <template slot-scope="scope">
       <el-input :id="memberInputId+scope.$index" @keyup.enter.native="enterNext(4, scope.$index)" v-model="scope.row.memberScore" placeholder="" ></el-input>
      </template>
    </el-table-column>
    <el-table-column
      label="战绩"
      width="100"
      align="center">
      <template slot-scope="scope">
       <el-input :id="recordInputId+scope.$index" @keyup.enter.native="enterNext(5, scope.$index)" v-model="scope.row.record" placeholder="战绩" v-on:change="computeZJ(scope.$index, true, false)"></el-input>
      </template>
    </el-table-column>
    <el-table-column
      label="保险"
      width="80"
      align="center">
      <template slot-scope="scope">
       <el-input :id="bxInputId+scope.$index" @keyup.enter.native="enterNext(6, scope.$index)" v-on:change="computeBX(scope.$index, true, true, false)" v-model="scope.row.baoxian" placeholder="保险"></el-input>
      </template>
    </el-table-column>
     <el-table-column
        label="战绩结算"
        width="90"
        align="center">
      <template slot-scope="scope">
       <el-input :id="zjjsInputId+scope.$index" @keyup.enter.native="enterNext(7, scope.$index)" v-model="scope.row.zhanjirs" placeholder="" v-on:change="computeTotal(scope.$index,false)"></el-input>
      </template>
    </el-table-column>
     <el-table-column
        label="保险结算"
        width="90"
        align="center">
      <template slot-scope="scope">
       <el-input :id="bxjsInputId+scope.$index" @keyup.enter.native="enterNext(8, scope.$index)" v-model="scope.row.baoxianrs" placeholder="" v-on:change="computeTotal(scope.$index,false)"></el-input>
      </template>
    </el-table-column>
    <el-table-column
        label="总额"
        width="100"
        align="center">
      <template slot-scope="scope">
       <el-input :id="totalInputId+scope.$index" @keyup.enter.native="enterNext(9, scope.$index)" v-model="scope.row.total" placeholder="总额"></el-input>
      </template>
    </el-table-column>
    <el-table-column
        prop="rid"
        label="推荐人"
        width="140"
        align="center">
    </el-table-column>
    <el-table-column
        label="推荐人结算"
        width="100"
        align="center">
      <template slot-scope="scope">
       <el-input :id="tjrjsInputId+scope.$index" @keyup.enter.native="enterNext(10, scope.$index)" v-if="scope.row.isShowReferrer" v-model="scope.row.rgain" placeholder=""></el-input>
      </template>
    </el-table-column>
  <el-table-column
      label="是否结算"
      width="80"
      align="center">
      <template slot-scope="scope">
       <el-select v-model="scope.row.isSettled">
         <el-option v-for="item in scope.row.jiesuan" :key="item.label" :label="item.label" :value="item.value">
         </el-option>
       </el-select>
      </template>
    </el-table-column>
</el-table> -->
                </el-tab-pane>
            </el-tabs>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'tabs',
        data() {
            return {
                activeName:'first',
                types: [],
                classid:'',
                name:'',
                price_desc:'',
                price:'',
                rush_price:'',
                rush_price_desc:'',
                goods_desc:'',
                brand:'',
                sort_id:'',
                imgUrl:'',
                querying:false,
                updateGoodsId:22,
                level:[{count:'',time:'',difficulty:''},{count:'',time:'',difficulty:''},{count:'',time:'',difficulty:''}],
                tableData:[]
            }
        },
        mounted: function () {
          this.querying = true
           this.$axios.get(this.global.serverPath + '/app/goodsclass')
           .then(res => {
           this.types = res['data']['data']
           this.classid = this.types[0].classid
           this.querying = false
          })
          .catch(err => {
           this.$message.error(err)
           this.querying = false
          })
        },
        methods: {
             chooseImg: function () {
               document.getElementById("file").click()
             },
              commit: function () {
              if (this.imgUrl === ''){
                this.$message.error('没有选择图片')
                return
              }
              if (this.name === ''){
                this.$message.error('商品名不能为空')
                return
              }
              if (this.price_desc === ''){
                this.$message.error('价格描述不能为空')
                return
              }
              var tmp = this.price
              if (!this.global.isNumber(tmp)){
                this.$message.error('价格格式错误')
                return
              }
              var price = parseInt(tmp)
              if (price <=0){
                 this.$message.error('价格数值不正确')
                 return
             }
             tmp = this.rush_price
              if (!this.global.isNumber(this.rush_price)){
                this.$message.error('闯关价格式错误')
                return
              }
              var rush_price = parseInt(tmp)
              if (rush_price <=0){
                 this.$message.error('闯关价数值不正确')
                 return
              }

              if (this.rush_price_desc === ''){
                this.$message.error('闯关价描述不能为空')
                return
              }
              if (this.goods_desc === ''){
                this.$message.error('色号不能为空')
                return
              }
              if (this.brand === ''){
                this.$message.error('品牌不能为空')
                return
              }

              tmp = this.sort_id
              if (!this.global.isNumber(this.sort_id)){
                this.$message.error('排序id格式错误')
                return
              }
              var sort_id = parseInt(tmp)
              if (sort_id <0){
                 this.$message.error('排序id数值不正确')
                 return
              }

              var new_level=new Array()
              for (var i = 0;i<3;i++) {
                var obj = {count:0,time:0,difficulty:0}
                tmp = this.level[i].count
                if (!this.global.isNumber(tmp)){
                  this.$message.error('第'+(i+1)+'关口红数格式错误')
                  return
                }
                var value = parseInt(tmp)
                if (value <=0){
                   this.$message.error('第'+(i+1)+'关口红数值不正确')
                   return
                }
                obj.count = value

                tmp = this.level[i].time
                if (!this.global.isNumber(tmp)){
                  this.$message.error('第'+(i+1)+'关游戏时间格式错误')
                  return
                }
                var value = parseInt(tmp)
                if (value <=0){
                   this.$message.error('第'+(i+1)+'关游戏时间数值不正确')
                   return
                }
                obj.time = value

                tmp = this.level[i].difficulty
                if (!this.global.isNumber(tmp)){
                  this.$message.error('第'+(i+1)+'关难度系数格式错误')
                  return
                }
                var diff = parseInt(tmp)
                if (diff < 0 || diff>100){
                    this.$message.error('第'+(i+1)+'关难度系数超出范围')
                    return
                }
                obj.difficulty = parseInt(diff)
                new_level.push(obj)
              }
              
              
               this.$confirm('是否确认提交数据?', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning',
        center: true
      }).then(() => {
        this.querying = true
        var arr=this.imgUrl.split(",")
        var post_imgUrl=arr[1]
        var json = {level:new_level,goodsid:this.updateGoodsId,base64str:post_imgUrl,name: this.name, classid: this.classid, sortid: sort_id, pricedesc: this.price_desc,price: price,rushprice:rush_price,rushpricedesc:this.rush_price_desc,goodsdesc:this.goods_desc,brand:this.brand}
        this.$axios.post(this.global.serverPath + '/web/editgoods', JSON.stringify(json))
        .then(res => {
            var code = res['data']['code']
            var msg = this.global.codeError[code]
            if (msg === undefined) {
              this.$message({message: '提交成功', type: 'success'})
            } else {
              this.$message.error(msg)
            }
            this.querying = false
          })
          .catch(err => {
            this.$message.error(err)
            this.querying = false
          })
      }).catch(() => {
      })

             },
             update: function (e) {
                var file = e.target.files[0]
                var reader = new FileReader()
                var that = this
                reader.readAsDataURL(file)
                reader.onload = function(e) {
                    that.imgUrl = this.result
                }
             }
        }
    }

</script>

<style>
.message-title{
    cursor: pointer;
}
.handle-row{
    margin-top: 30px;
}
.cinput{
    width: 600px;
}
.cselect{
    width: 100
    px;
}

</style>

