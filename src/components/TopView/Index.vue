<template>
  <div>
    <el-row :gutter="20">
      <el-col :span="6">
        <el-card shadow="hover">
          <TotlaSales />
        </el-card>
      </el-col>
      <el-col :span="6">
        <el-card shadow="hover">
          <TotlaOrders />
        </el-card>
      </el-col>
      <el-col :span="6">
        <el-card shadow="hover">
          <TodayUser />
        </el-card>
      </el-col>
      <el-col :span="6">
        <el-card shadow="hover">
          <TotlaUsers />
        </el-card>
      </el-col>
    </el-row>
    
  </div>
</template>

<script>
import TotlaSales from './TotlaSales/Index'
import TotlaOrders from './TotlaOrders/Index'
import TodayUser from './TodayUser/Index'
import TotlaUsers from './TotlaUsers/Index'


export default {
  components: { TotlaSales, TotlaOrders, TodayUser, TotlaUsers },
  data() {
    return {
      
    };
  },
  methods: {
    
  },
  mounted() {
    
  },
}
</script>

<style lang='scss' scoped>

</style>