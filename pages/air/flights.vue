<template>
    <section class="contianer">
        <el-row  type="flex" justify="space-between">

            <!-- 顶部过滤列表 -->
            <div class="flights-content">
                <!-- 过滤条件 -->
                <div>
                    
                </div>
                
                <!-- 航班头部布局 -->
                <FlightsListHead/>
                    
                
                
                
                <!-- 航班信息 -->
                
                <!-- 列表 -->
                    <FlightsItem
                    v-for="(item,index) in dataList"
                    :key="index"
                    :data="item"
                    />
                    <!-- 分页 -->
                     <el-row type="flex" justify="center" style="margin-top:10px;">
                        <!-- size-change：切换条数时候触发 -->
                        <!-- current-change：选择页数时候触发 -->
                        <!-- current-page: 当前页数 -->
                        <!-- page-size：当前条数 -->
                        <!-- total：总条数 -->
                        <el-pagination
                        @size-change="handleSizeChange"
                        @current-change="handleCurrentChange"
                        :current-page="pageIndex"
                        :page-sizes="[5, 10, 15, 20]"
                        :page-size="pageSize"
                        layout="total, sizes, prev, pager, next, jumper"
                        :total="flightsData.total">
                        </el-pagination>
                    </el-row>
                
            </div>

            <!-- 侧边栏 -->
            <div class="aside">
                <!-- 侧边栏组件 -->
            </div>
        </el-row>
    </section>
</template>

<script>

import FlightsListHead from "@/components/air/flightsListHead.vue"
import FlightsItem from "@/components/air/flightsItem.vue"
export default {
    data(){
        return {
            //航班总数据
            flightsData:{
                flights: []
            },
            //航班列表数据
           dataList:[],
           pageIndex:1,//当前页数
           pageSize:5,//显示条数
           total:0
        }
    },
    methods: {
        handleSizeChange(value){
            this.pageSize=value
            //重回第一页
            this.pageIndex=1;
            //设置显示数据列表
            this.setDataList()
        },
        //页数切换时候触发
        handleCurrentChange(value){
            this.pageIndex=value;
            this.setDataList()
        },
        //设置显示数据列表
       setDataList(){
            // 截图当前页面显示数据
            // 0,5
            // 5, 10
            // 10, 15
            this.dataList = this.flightsData.flights.slice(
                (this.pageIndex - 1) * this.pageSize,
                this.pageIndex * this.pageSize
            )
        },
           // 切换条数时触发
        handleSizeChange(value){
            this.pageSize = value;
            this.pageIndex = 1;
            this.setDataList();
        },

        // 切换页数时触发
        handleCurrentChange(value){
            this.pageIndex = value;
            this.setDataList();
        },



       
    },
    mounted () {
        // 请求机票列表
        this.$axios({
            url: "/airs",
            params: this.$route.query
        }).then(res => {
            // 总数据，（flights, info, options, total）
            this.flightsData = res.data;
            // 总条数
            this.total = this.flightsData.flights.length;

            // 第一页的数据
            this.setDataList();
        })
    },
    components: {
        FlightsListHead,
        FlightsItem
    }
}
</script>

<style scoped lang="less">
    .contianer{
        width:1000px;
        margin:20px auto;
    }

    .flights-content{
        width:745px;
        font-size:14px;
    }

    .aside{
        width:240px;
    } 
</style>