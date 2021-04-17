<template>
  <div>
    <CommonCard 
      title="累计销售额"
      value="32,039,165"
    >
      <template>
        <div class="compare">
          <span>日同比</span>
          <span>7.33%</span>
          <span class="increase"></span>
        </div>
        <div class="compare">
          <span>月同比</span>
          <span>7.33%</span>
          <span class="decrease"></span>
        </div>
      </template>
      <template v-slot:footer>
        <span>昨日销售额</span>
        <span>¥ 30,000,000</span>
      </template>
    </CommonCard>
  </div>
</template>

<script>
import commonCardMixin from '../../../mixins/commonCardMixin'

export default {
  mixins:[commonCardMixin],
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
.compare{
  display: flex;
  align-items: center;
  font-size: 12px;
  line-height: 24px;
  .increase {
    width: 0;
    height: 0;
    border-width: 3px;
    border-color: transparent transparent red transparent;
    border-style: solid;
    margin:  0 0 3px 5px;
  }
  .decrease {
    width: 0;
    height: 0;
    border-width: 3px;
    border-color: green transparent transparent transparent;
    border-style: solid;
    margin:  3px 0 0 5px;
  }
}
.money{
  margin-left: 5px;
  color: #000;
  font-weight: 700;
}
</style>