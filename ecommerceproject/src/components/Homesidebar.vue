<template>
    <div>
        <div class="col-md-3">
                  <!-- 左側選單 (List group) -->
                  <div class="list-group sticky-top" >
                    <router-link class="list-group-item list-group-item-action active" data-toggle="list"  to="/home" >
                      <i class="fa fa-suitcase" aria-hidden="true"></i> 工作坊</router-link>
                    <router-link class="list-group-item list-group-item-action active" data-toggle="list"  to="/customer_orders_b">
                      <i class="fa fa-suitcase" aria-hidden="true"></i> 直播活動 </router-link>
                    <router-link class="list-group-item list-group-item-action active" data-toggle="list"  to="/customer_orders_c">
                      <i class="fa fa-suitcase" aria-hidden="true"></i> 課程 </router-link>
                   
                  </div>
        </div>
    </div>
</template>