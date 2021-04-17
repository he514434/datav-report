<template>
  <div class="home">
    <TopView />
    <SalesView />
    <BottomView />
    <MapView />
  </div>
</template>
<script>

import TopView from '../components/TopView/Index'
import SalesView from '../components/SalesView/Index'
import BottomView from '../components/BottomView/Index'
import MapView from '../components/MapView/Index'

export default {
  components: { TopView, SalesView, BottomView, MapView },
  data () {
    return {

    }
  }
}
</script>

<style>
 .home {
   width: 100%;
   height: 100%;
   padding: 20px;
   background: #eee;
   box-sizing: border-box;
 }
</style>
