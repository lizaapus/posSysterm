<template>
    <div class='Pos'>
        <el-row >
            <el-col :span='7' class='order1' >
                <el-tabs class='el-table-class'>
                    <el-tab-pane  label="点餐" id='OrderTab' border style="width:100%">
                        <el-table :data='orderData' border show-summary :summary-method='getSummary'>
                            <el-table-column prop='goodsName' label='商品名称' >
                            </el-table-column>
                            <el-table-column prop='count' label='数量' width='70'>

                            </el-table-column>
                            <el-table-column prop='price' label='单价' width='70'>

                            </el-table-column>
                            <el-table-column prop='money' label='金额' width='70'>

                            </el-table-column>


                            <el-table-column label='操作' width='100' align='center'  fixed="right">
                                <template slot-scope="scope">
                                     <el-button type='text' size='small'>
                                         <i class="el-icon-plus" style="color:#67C23A" @click="addGoods(scope.row)"></i>
                                    </el-button>
                                    <el-button type='text' size='small'>
                                         <i class="el-icon-minus" style="color:#E6A23C" @click="minusGoods(scope.row)"></i>
                                    </el-button>
                                    <el-button type='text' size='small'>
                                        <i class="el-icon-delete" style="color:#F56C6C" @click="deleteGoods(scope.row)"></i>
                                    </el-button>
                                </template>
                            </el-table-column>
                        </el-table>
                        <div class='divButton' >
                            <el-button type='success'>结账</el-button>
                            <el-button type='warning'>挂单</el-button>
                            <el-button type='danger'>取消订单</el-button>
                        </div>
                        
                    </el-tab-pane>
                    <el-tab-pane label='挂单' id='CheckTab' >

                    </el-tab-pane>
                    <el-tab-pane label='外卖' id='TkeOutOrderTab' >

                    </el-tab-pane>
                </el-tabs>
            </el-col>
            <el-col :span='17' class='order2' >
               <div class="bestSellers">
                    <div class="title">热卖</div>
                    <div class="bestSellerDiv">
                        <ul>
                            <li v-for="dish in bestSellerData" class='foodli' @click="addGoods(dish)" >
                                <span>
                                    <img :src='dish.picUrl'  class='foodImg'/>
                                </span> 
                                <div class="priceDiv">
                                    <span v-text='dish.goodsName' class='foodName'></span>
                                    <span  class='price'>￥<span  v-text='dish.price'></span>元</span>  
                                </div> 
                               
                            </li>
                        </ul>
                    </div> 
               </div>
               <div class='Types'>
                   <el-tabs>
                    <el-tab-pane label="热菜"  border style="width:100%">
                        <div class="bestSellerDiv">
                            <ul>
                                <li v-for="hotdish in hotDishesData" class='foodli' @click="addGoods(hotdish)" >
                                    <span>
                                        <img :src='hotdish.picUrl'  class='foodImg'/>
                                    </span>  
                                    <span v-text='hotdish.goodsName' class='foodName'></span>
                                    <span  class='price'>￥<span  v-text='hotdish.price'></span>元</span>  
                                </li>
                            </ul>
                        </div>
                    </el-tab-pane>
                    <el-tab-pane label='凉菜' class='coldDishes'>
                        <div class="bestSellerDiv">
                            <ul>
                                <li v-for="colddish in coldDishesData" class='foodli' @click="addGoods(colddish)">
                                    <span>
                                        <img :src='colddish.picUrl'  class='foodImg'/>
                                    </span>  
                                    <span v-text='colddish.goodsName' class='foodName'></span>
                                    <span class='price'>￥<span  v-text='colddish.price'></span>元</span>  
                                </li>
                            </ul>
                        </div>
                    </el-tab-pane>
                    <el-tab-pane label='饮料' class='drinks'>
                         <div class="bestSellerDiv">
                            <ul>
                                <li v-for="drink in drinksData" class='foodli'  @click="addGoods(drink)">
                                    <span>
                                        <img :src='drink.picUrl'  class='foodImg'/>
                                    </span>  
                                    <span v-text='drink.goodsName' class='foodName'></span>
                                    <span  class='price'>￥<span  v-text='drink.price'></span>元</span>  
                                </li>
                            </ul>
                        </div>
                    </el-tab-pane>
                    <el-tab-pane label='主食' class='stapleFood'>
                        <div class="bestSellerDiv">
                            <ul>
                                <li v-for="staple in stapleFoodData" class='foodli' @click="addGoods(staple)" >
                                    <span>
                                        <img :src='staple.picUrl'  class='foodImg'/>
                                    </span>  
                                    <span v-text='staple.goodsName' class='foodName'></span>
                                    <span  class='price'>￥<span  v-text='staple.price'></span>元</span>  
                                </li>
                            </ul>
                        </div>
                    </el-tab-pane>
                </el-tabs>
               </div>
            </el-col>
        </el-row>
    </div>
</template>
<script>
export default {
    name:'Pos',
    data(){
        return{
           orderData:[
           ],
           bestSellerData:[
               {
                   goodsId:1,
                   goodsName:'宫保鸡丁',
                   picUrl:'https://fuss10.elemecdn.com/e/e5/887f40ee45625eb3d92eaafdf2ea3jpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                   price:38
               },
                {
                   goodsId:2,
                   goodsName:'尖椒肉丝',
                   picUrl:'https://fuss10.elemecdn.com/7/e6/313c2b6b344425278a3957c9dc27ejpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                   price:38
               },
                {
                   goodsId:3,
                   goodsName:'泡椒腰花',
                   picUrl:'https://fuss10.elemecdn.com/7/fd/9fcc1c6e94f20178deadd94576dabjpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                   price:42 
               },
                 {
                    goodsId:4,
                    goodsName:'南瓜饼',
                    picUrl:'https://fuss10.elemecdn.com/d/e2/f38ec7e8596cf3df06f21dcb40ca0jpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                    price:20
               },
                {
                   goodsId:5,
                   goodsName:'炖腔骨',
                   picUrl:'https://fuss10.elemecdn.com/d/49/15e9a53c095168661ad973f127ae9jpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                   price:62
               },
                {
                    goodsId:6,
                    goodsName:'酸辣木耳',
                    picUrl:'https://fuss10.elemecdn.com/e/9a/4c6215d464b2793a51558f4e30865jpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                    price:22
               },
               {
                    goodsId:7,
                    goodsName:'花椒拌凉鸡',
                    picUrl:'https://fuss10.elemecdn.com/3/83/a9ce992ec978b578515b4bd965f09jpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                    price:42
               },
               {
                    goodsId:8,
                    goodsName:'米酒',
                    picUrl:'https://fuss10.elemecdn.com/9/4b/fc454ab9961731a4f984664bb2d83png.png?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                    price:20
               },
               {
                    goodsId:9,
                    goodsName:'野生酸角树莓汁',
                    picUrl:'https://fuss10.elemecdn.com/9/b1/1e0b00a45a8037d9fbe94fef0a5acjpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                    price:28
               },
               
           ],
           hotDishesData:[
               {
                   goodsId:1,
                   goodsName:'宫保鸡丁',
                   picUrl:'https://fuss10.elemecdn.com/e/e5/887f40ee45625eb3d92eaafdf2ea3jpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                   price:38
               },
                {
                   goodsId:2,
                   goodsName:'尖椒肉丝',
                   picUrl:'https://fuss10.elemecdn.com/7/e6/313c2b6b344425278a3957c9dc27ejpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                   price:38
               },
                {
                   goodsId:3,
                   goodsName:'泡椒腰花',
                   picUrl:'https://fuss10.elemecdn.com/7/fd/9fcc1c6e94f20178deadd94576dabjpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                   price:42 
               },
                {
                   goodsId:4,
                   goodsName:'焦溜丸子',
                   picUrl:'https://fuss10.elemecdn.com/2/cd/b69094144ad7144b0d4d4ebf4ce80jpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                   price:38
               },
                {
                   goodsId:5,
                   goodsName:'炖腔骨',
                   picUrl:'https://fuss10.elemecdn.com/d/49/15e9a53c095168661ad973f127ae9jpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                   price:62
               },
                {
                   goodsId:6,
                   goodsName:'火爆鸡胗',
                   picUrl:'https://fuss10.elemecdn.com/2/e7/f7fb04b8ac9ece5c9d266d7835d1bjpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                   price:35
               },
                {
                   goodsId:7,
                   goodsName:'茶树菇炒肉丝',
                   picUrl:'https://fuss10.elemecdn.com/5/7e/f7c993b4586243ffedce97c395fc2jpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                   price:32
               },
                {
                   goodsId:8,
                   goodsName:'红烧排骨',
                   picUrl:'https://fuss10.elemecdn.com/7/a8/b282d4746987a71e4371ee18b0736jpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                   price:42
               },
               {
                   goodsId:9,
                   goodsName:'白灼菜心',
                   picUrl:'https://fuss10.elemecdn.com/6/71/dce237420401ede8f42904a30085fpng.png?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                   price:28
               },
               {
                    goodsId:10,
                    goodsName:'莴苣炒山药',
                    picUrl:'https://fuss10.elemecdn.com/3/a6/c241638bd299caa5b7a81489d4fb3png.png?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                    price:27
               },
               {
                    goodsId:11,
                    goodsName:'五彩时蔬',
                    picUrl:'https://fuss10.elemecdn.com/3/21/a506392df7d575cf8e3dd423598aejpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                    price:32
               },
               {
                    goodsId:12,
                    goodsName:'皱皮椒土豆丝',
                    picUrl:'https://fuss10.elemecdn.com/a/db/3a8739881f1d90c3f5ba93848eba1png.png?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                    price:16
               }
           ],
           coldDishesData:[
               {
                    goodsId:1,
                    goodsName:'青柠檬拌鲜菠萝',
                    picUrl:'https://fuss10.elemecdn.com/f/98/3d8e5752809f8797399c431e4684ejpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                    price:15
               },
               {
                    goodsId:2,
                    goodsName:'手撕美人椒拌牛肉',
                    picUrl:'https://fuss10.elemecdn.com/8/65/ba9dcbe014e3d9dfccc9e800ebcc8jpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                    price:42
               },
               {
                    goodsId:3,
                    goodsName:'版纳拌折耳根',
                    picUrl:'https://fuss10.elemecdn.com/d/07/9fbb89ba7d55f980c9bde4da3c13ajpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                    price:19
               },
               {
                    goodsId:4,
                    goodsName:'酸辣秋葵',
                    picUrl:'https://fuss10.elemecdn.com/8/87/3b6b0c54044f230cbf75972257b99jpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                    price:28
               },
               {
                    goodsId:5,
                    goodsName:'酸辣木耳',
                    picUrl:'https://fuss10.elemecdn.com/e/9a/4c6215d464b2793a51558f4e30865jpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                    price:22
               },
               {
                    goodsId:6,
                    goodsName:'花椒拌凉鸡',
                    picUrl:'https://fuss10.elemecdn.com/3/83/a9ce992ec978b578515b4bd965f09jpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                    price:42
               },
               
           ],
           drinksData:[
               {
                    goodsId:1,
                    goodsName:'米酒',
                    picUrl:'https://fuss10.elemecdn.com/9/4b/fc454ab9961731a4f984664bb2d83png.png?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                    price:20
               },
               {
                    goodsId:2,
                    goodsName:'野生酸角树莓汁',
                    picUrl:'https://fuss10.elemecdn.com/9/b1/1e0b00a45a8037d9fbe94fef0a5acjpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                    price:28
               },
               {
                    goodsId:3,
                    goodsName:'炸果果',
                    picUrl:'https://fuss10.elemecdn.com/5/76/096b9b4851ca656d9409690f2fcc3png.png?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                    price:29
               },
               {
                    goodsId:4,
                    goodsName:'青柠火龙果汁',
                    picUrl:'https://fuss10.elemecdn.com/4/a2/be2019a409caa9ea2267d25b3aebdjpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                    price:28
               },
               {
                    goodsId:5,
                    goodsName:'鲜榨西瓜汁',
                    picUrl:'https://fuss10.elemecdn.com/9/72/d79cb642493988888f40f77c2d754jpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                    price:28
               },
               {
                    goodsId:6,
                    goodsName:'加多宝',
                    picUrl:'https://fuss10.elemecdn.com/1/b1/1948dce1c32d818dcb491ee69ac4cjpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                    price:10
               },
           ],
           stapleFoodData:[
               {
                    goodsId:1,
                    goodsName:'金银馒头',
                    picUrl:'https://fuss10.elemecdn.com/3/98/5041125af4faacb5ac70bebb1afd5jpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                    price:18
               },
               {
                    goodsId:2,
                    goodsName:'南瓜饼',
                    picUrl:'https://fuss10.elemecdn.com/d/e2/f38ec7e8596cf3df06f21dcb40ca0jpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                    price:20
               },
               {
                    goodsId:3,
                    goodsName:'麻团',
                    picUrl:'https://fuss10.elemecdn.com/f/65/82e2688cdcbd229f64132aabe6ea4jpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                    price:20
               },
               {
                    goodsId:4,
                    goodsName:'手工水饺',
                    picUrl:'https://fuss10.elemecdn.com/1/ce/e28de75d1bb4372e74ffdac435aecjpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                    price:18
               },
              
               {
                    goodsId:5,
                    goodsName:'香芋卷',
                    picUrl:'https://fuss10.elemecdn.com/8/fc/67c152fb2e79b18433d9644d484c4jpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                    price:20
               },
               {
                    goodsId:6,
                    goodsName:'米饭',
                    picUrl:'https://fuss10.elemecdn.com/8/75/6fce876c46eb749726f9330fd58c4jpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                    price:3
               },
               {
                    goodsId:7,
                    goodsName:'韭菜鸡蛋水饺',
                    picUrl:'https://fuss10.elemecdn.com/5/c9/721000b3ebf4392b85ece12140ac1jpeg.jpeg?imageMogr2/thumbnail/200x200/format/webp/quality/85',
                    price:18
               },
           ],
        }
    },
    methods:{
        addGoods(newdish){
            let isHave=false;
            this.orderData.forEach(element => {
                if(element.goodsName==newdish.goodsName){
                    isHave=true;
                    element.count++;
                    element.money = element.count*element.price;
                    return;
                }
            });
            if(!isHave)
            {
                let l = {goodsName:newdish.goodsName,count:1,price:newdish.price,money:newdish.price};
                this.orderData.push(l);
            }
        },
        minusGoods(delGoods){
            this.orderData.forEach(element => {
                if(element.goodsName==delGoods.goodsName){
                    element.count--;
                    element.money = element.count*element.price;  
                }
            });
            this.orderData = this.orderData.filter((e)=>e.count!=0);
        },
        deleteGoods(delgoods){
            this.orderData = this.orderData.filter((e)=>e.goodsName!=delgoods.goodsName);
        },

        getSummary(param){
            const{columns,data} = param;
            const sums = [];
            columns.forEach((column,index)=>{
                if(index===0){
                    sums[index]='合计';
                    return;
                }
                if(column.label=='单价')
                {
                    sums[index]=" ";
                    return;
                }
               
                const values = data.map(item=>Number(item[column.property]));
                if(!values.every(value=>isNaN(value))){
                   sums[index] = values.reduce((prev,curr)=>{
                        const value = Number(curr);
                        if(!isNaN(value)){
                            return prev+curr;
                        }else{
                            return prev;
                        }
                        },0);

                    if(column.label=='金额')
                        sums[index]+='元';
                }else{
                    sums[index]=' ';
                }


            });

            return sums;
        }

    }
}
</script>

<style scoped>
.Pos{
    height: 100%;
    width: 100%;
    float: left;

}
.el-row{
    height: 100%;
}
.el-table-class{
    margin-left: 10px;
}
.order1{
    height: 100%;
    background-color:white;
    font-family: 'Courier New', Courier, monospace;
    font-size: 16px;
    font-weight: bolder;
}
.order2{
    height: 100%;
    float: left;
    background-color:whitesmoke;
}
.divButton{
    margin-top: 10px;
}

.bestSellers{
    float: left;
    height: auto;
    width: 100%;
}
.Types{
    float: left;
    width: 100%;
}
.Types ul li{
    list-style: none;
    float:left;
    border: 1px solid #d3dce6;
    margin: 10px;
    padding: 10px;
    background-color: #ffffff;
}

.title{
    height: 24px;
    margin-top: 20px;
    margin-bottom: -10px;
    color: red;
    font-weight: bolder;
    font-size: 18px;
}
.bestSellerDiv ul li{
    list-style: none;
    float:left;
    border: 1px solid #d3dce6;
    margin: 20px;
    padding: 10px;
    background-color: #ffffff;
    
}

.bestSellerDiv ul li{
    list-style: none;
    width: 20%;
    border:1px solid #e5e9f2;
    height: auto;
    overflow:hidden;
    background-color: white;
    padding: 2px;
    float: left;
    margin: 2px;
    cursor: pointer;
}

.hotDishes li span{
    display: block;
    float:left;
     cursor: pointer;
}
.foodli{
    display: block;
    float: left;
    width: 80px;
}

.foodImg{
    float: left;
    width:40px;
    height: 40px;
}

.foodName{
    float: left;
    font-size: 16px;
    margin-left: 9px;
    color: black;
    font-weight: bold;
}

.price{
    float:right;
    font-size: 16px;
    /* padding-left: 100px; */
    padding-top: 0px;
    color:rgb(184, 19, 19);
    font-weight: bolder;
}

</style>


