<template>
    <div>
        <div class="d-flex mb-4">
        </div>
        <loading :active.sync="isLoading"></loading>
        <div class="row mb-4 mt-4">
            <div class="col-md-4 mb-4" v-for="item in products" :key="item.id"  v-if="item.category==='工作坊'">
                <div class="card border-0 shadow-sm">
                    <div style="height: 150px; background-size: cover; background-position: center"
                    :style="{backgroundImage:`url(${item.imageUrl})`}"
                    >
                    </div>
                    <div class="card-body">
                    <span class="badge badge-secondary float-right ml-2">{{item.category}}</span>
                    <h5 class="card-title">
                        <a href="#" class="text-dark">{{item.title}}</a>
                    </h5>
                    <p class="card-text">{{item.content}}</p>
                    <div class="d-flex justify-content-between align-items-baseline">
                        <!-- <div class="h5">2,800 元</div> -->
                        <del class="h6">原價 {{item.origin_price}} 元</del>
                        <div class="h5">現在只要 {{item.price}} 元</div>
                    </div>
                    </div>
                    <div class="card-footer d-flex">
                    <router-link type="button" class="btn btn-outline-secondary btn-sm" to="/productdetail" @click="getProduct(item.id)">
                        <i class="fas fa-spinner fa-spin"  v-if="status.loadingItem === product.id"></i>
                        了解詳情
                    </router-link>
                    <button type="button" class="btn btn-outline-danger btn-sm ml-auto" @click="addtoCart(item.id)">
                        <i class="fas fa-spinner fa-spin"></i>
                        加到購物車
                    </button>
                    </div>
                </div>
            </div>
        </div>
        
       
        
        

        <!-- Modal -->
        <div class="modal fade" id="productModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
            <div class="modal-dialog">
                <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="exampleModalLabel">{{product.title}}</h5>
                    <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                    <span aria-hidden="true">&times;</span>
                    </button>
                </div>
                <div class="modal-body">
                    
                    <select name="" class="form-control mt-3" v-model="product.num">
                      <option :value="num" v-for="num in 10" :key="num">
                        選購{{num}} {{product.unit}}
                      </option>
                    </select>
                </div>
                <div class="modal-footer">
                  <div class="text-muted text-nowrap mr-3">
                    小計
                    <strong>
                      {{product.price * product.num}}
                    </strong>
                    元
                  </div>
                  <button type="button" class="btn btn-primary" @click="addtoCart(product.id, product.num)">
                    <i class="fas fa-spinner fa-spin"  v-if="status.loadingItem === product.id"></i>
                    加到購物車
                  </button>
                </div>
                </div>
            </div>
        </div>
        
    </div>
</template>

<script>
import $ from 'jquery'; //載入modal

export default {
  data() {
    return {
      products: [],
      product: {}, //存放查看更多的Modal資料
      isLoading: false,
      status: {
        loadingItem: '', //存放產品id
      },
      cart: {},
      pagination: {},
    }
  },
  methods: {
    getProducts(page=1){ //取得遠端資料的方法 //把Products存到宣告的products裡面 //將page傳進來 >> getProducts(page=1) 預設值帶第一頁進來
            const api = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/products?page=${page}`; //${page} 設定變數
            const vm = this; //確保資料存到vm裡面
            console.log(process.env.APIPATH,process.env.CUSTOMPATH);
            vm.isLoading = true;
            this.$http.get(api).then((response) => {
            console.log(response.data);
            vm.isLoading = false;
            vm.products = response.data.products; //可以用Vue檢查一下資料有沒有get到
            vm.pagination = response.data.pagination;
            })
     },
    
    getProduct(id) {
      const vm = this;
      const url = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/product/${id}`;
      // vm.isLoading = true;
      vm.status.loadingItem = id;
      this.$http.get(url).then((response) => {
        vm.product = response.data.product; //先讀取完資料後
        $('#productModal').modal('show'); //再將Modal打開
        console.log(response);
        // vm.isLoading = false;  
        vm.status.loadingItem = ''; //Modal打開後將值替換成空的
      });
    },
    // productDetail(id) {
    //   const vm = this;
    //   const url = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/product/${id}`;
    //   // vm.isLoading = true;
    //   vm.status.loadingItem = id;
    //   this.$http.get(url).then((response) => {
    //     vm.product = response.data.product; //先讀取完資料後
    //     console.log(response);
    //     // vm.isLoading = false;  
    //     vm.status.loadingItem = ''; //Modal打開後將值替換成空的
    //   });
    // },
    addtoCart(id,qty=1){ //ES6 預設值設定方法 qty=1
      const vm = this;
      const url = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/cart`;
      vm.status.loadingItem = id;
      const cart = { //定義資料結構
        product_id: id,
        qty,
      };
      this.$http.post(url, {data: cart}).then((response) => {
        console.log(response);
        vm.status.loadingItem = ''; //Modal打開後將值替換成空的
        vm.getCart(); //把購物車取得回來
        $('#productModal').modal('hide'); //加到購物車後關掉Modal
      });
    },
    getCart(){
      const vm = this;
      const url = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/cart`;
      vm.isLoading = true;
      this.$http.get(url).then((response) => {
        vm.cart= response.data.data;
        console.log(response);
        vm.isLoading = false;
      });
    },
    
    
  },
  created() { //取得資料要在這邊設定
    this.getProducts();
    this.getCart(); //把購物車取得回來
  },
};
</script>

