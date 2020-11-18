
<template>
  <div>
      <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
        <title>六角血拼賣賣</title>
        <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css">
        <!-- Bootstrap CSS -->
        <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.1/css/bootstrap.min.css" integrity="sha384-WskhaSGFgHYWDcbwN70/dfYBj47jz9qbsMId/iRN3ewGhXQFZCSftd1LZCfmhktB"
          crossorigin="anonymous">
        <link rel="stylesheet" href="custom.css">

      </head>

      <body>
        
            <!-- headers -->
            <nav class="navbar navbar-light bg-light">
              <a class="navbar-brand" href="shoppingCart.html">
                <i class="fa fa-heart text-info" aria-hidden="true"></i>
                六角血拼賣賣
              </a>
              <!-- 購物車內的數量 (Button 內包含 icon, 數量 badge) -->
              <div class="dropdown ml-auto">
                <router-link to="/login" class="nav-link">
                登入
                </router-link>
                <button class="btn btn-sm btn-cart" data-toggle="dropdown" data-flip="false">
                  <i class="fa fa-shopping-cart text-dark fa-2x" aria-hidden="true"></i>
                  <span class="badge badge-pill badge-danger">9</span>
                  <span class="sr-only">unread messages</span>
                </button>
                <div class="dropdown-menu dropdown-menu-right p-3" style="min-width: 300px" data-offset="400">
                  <h6>已選擇商品</h6>
                  <table class="table table-sm">
                    <tbody>
                      <tr>
                        <td class="align-middle text-center">
                          <a href="#removeModal" class="text-muted" data-toggle="modal" data-title="刪除 金牌西裝 1 件">
                            <i class="fa fa-trash-o" aria-hidden="true"></i>
                          </a>
                        </td>
                        <td class="align-middle">金牌西裝</td>
                        <td class="align-middle">1 件</td>
                        <td class="align-middle text-right">$520</td>
                      </tr>
                      <tr>
                        <td class="align-middle text-center">
                          <a href="#removeModal" class="text-muted" data-toggle="modal" data-title="刪除 金牌女裝 1 件">
                            <i class="fa fa-trash-o" aria-hidden="true"></i>
                          </a>
                        </td>
                        <td class="align-middle">金牌女裝</td>
                        <td class="align-middle">1 件</td>
                        <td class="align-middle text-right">$480</td>
                      </tr>
                    </tbody>
                  </table>
                  <a href="shoppingCart-checkout.html" class="btn btn-primary btn-block">
                    <i class="fa fa-cart-plus" aria-hidden="true"></i> 結帳去
                  </a>
                </div>
              </div>
            </nav>
            <div class="jumbotron jumbotron-fluid jumbotron-bg d-flex align-items-end">
              <div class="container">
                <div class="p-3 bg-lighter">
                  <h1 class="display-3 font-weight-bold">買到剁手手！最後出清</h1>
                  <p class="lead">This is a modified jumbotron that occupies the entire horizontal space of its parent.</p>
                </div>
              </div>
            </div>
            <div class="container main-contant mb-1">
              <div class="row">
                <div class="col-md-3">
                  <!-- 左側選單 (List group) -->
                  <div class="list-group sticky-top">
                    <a class="list-group-item list-group-item-action active" data-toggle="list" href="#list-gold">
                      <i class="fa fa-suitcase" aria-hidden="true"></i> 金牌專賣店</a>
                    <a class="list-group-item list-group-item-action" data-toggle="list" href="#list-gift">
                      <i class="fa fa-gift" aria-hidden="true"></i> 禮品區</a>
                    <a href="#" class="list-group-item list-group-item-action disabled">
                      <i class="fa fa-film" aria-hidden="true"></i> 影音商品</a>
                    <a href="#" class="list-group-item list-group-item-action disabled">
                      <i class="fa fa-paw" aria-hidden="true"></i> 寵物專用</a>
                    <a href="#" class="list-group-item list-group-item-action disabled">
                      <i class="fa fa-tree" aria-hidden="true"></i> 居家環境</a>
                  </div>
                </div>
                <div class="col-md-9">
                  <div class="d-flex mb-4">
                    <!-- Search bar -->
                    <form class="form-inline my-3 my-lg-0">
                      <div class="input-group">
                        <input class="form-control" type="text" placeholder="Search" aria-label="Search">
                        <div class="input-group-append">
                          <button class="btn btn-outline-warning" type="submit">
                            <i class="fa fa-search" aria-hidden="true"></i> Search</button>
                        </div>
                      </div>
                    </form>
                  </div>
                  <!-- 載入管理員新增商品選項 -->
                  <loading :active.sync="isLoading"></loading>
                  <div class="row mb-4 mt-4">
                        <div class="col-md-4 mb-4" v-for="item in products" :key="item.id">
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
                                <button type="button" class="btn btn-outline-secondary btn-sm" @click="getProduct(item.id)">
                                    <i class="fas fa-spinner fa-spin"  v-if="status.loadingItem === product.id"></i>
                                    查看更多
                                </button>
                                <button type="button" class="btn btn-outline-danger btn-sm ml-auto" @click="addtoCart(item.id)">
                                    <i class="fas fa-spinner fa-spin"></i>
                                    加到購物車
                                </button>
                                </div>
                            </div>
                        </div>
                  </div>
                  <!-- 主要商品列表 (Card) -->
                  <div class="tab-content">
                    <div class="tab-pane active" id="list-gold">
                      <div class="row">
                        <!-- 金牌 -->
                        <div class="col-md-4 mb-4">
                          <div class="card border-0 box-shadow text-center h-100">
                            <img class="card-img-top" src="https://images.unsplash.com/photo-1494281258937-45f28753affd?w=1350" alt="Card image cap">
                            <div class="card-body">
                              <h4 class="card-title">金牌西裝</h4>
                              <p class="card-text">This is a longer card with supporting text below as a natural lead-in to additional content. This content
                                is a little bit longer.</p>
                              <p class="card-text">This is a longer card with supporting text below as a natural lead-in to additional content. This content
                                is a little bit longer.</p>
                            </div>
                            <div class="card-footer border-top-0 bg-white">
                              <div class="btn-group btn-group-sm">
                                <a href="shoppingCart-product.html" class="btn btn-outline-secondary">
                                  SM
                                </a>
                                <a href="shoppingCart-product.html" class="btn btn-outline-secondary">
                                  M
                                </a>
                                <a href="shoppingCart-product.html" class="btn btn-outline-secondary disabled">
                                  L
                                </a>
                                <a href="shoppingCart-product.html" class="btn btn-outline-secondary">
                                  XL
                                </a>
                              </div>
                            </div>
                          </div>
                        </div>

                        <div class="col-md-4 mb-4">
                          <div class="card border-0 box-shadow text-center h-100">
                            <img class="card-img-top" src="https://images.unsplash.com/photo-1481399124169-87493351c8a1?w=1349" alt="Card image cap">
                            <div class="card-body">
                              <h4 class="card-title">金牌女裝</h4>
                              <p class="card-text">This is a longer card with supporting text below as a natural lead-in to additional content. This content
                                is a little bit longer.</p>
                            </div>
                            <div class="card-footer border-top-0 bg-white">
                              <div class="btn-group btn-group-sm">
                                <a href="#" class="btn btn-outline-secondary">
                                  SM
                                </a>
                                <a href="#" class="btn btn-outline-secondary">
                                  M
                                </a>
                                <a href="#" class="btn btn-outline-secondary">
                                  L
                                </a>
                                <a href="#" class="btn btn-outline-secondary">
                                  XL
                                </a>
                              </div>
                            </div>
                          </div>
                        </div>

                        <div class="col-md-4 mb-4">
                          <div class="card border-0 box-shadow text-center h-100">
                            <img class="card-img-top" src="https://images.unsplash.com/photo-1486250944723-86bca2b15b06?w=1351" alt="Card image cap">
                            <div class="card-body">
                              <h4 class="card-title">特工眼鏡</h4>
                              <p class="card-text">This is a longer card with supporting text below as a natural lead-in to additional content. This content
                                is a little bit longer.</p>
                            </div>
                            <div class="card-footer border-top-0 bg-white">
                              <a href="#" class="btn btn-outline-secondary btn-block btn-sm">
                                <i class="fa fa-cart-plus" aria-hidden="true"></i> 搶購去
                              </a>
                            </div>
                          </div>
                        </div>

                        <div class="col-md-4 mb-4">
                          <div class="card border-0 box-shadow text-center h-100">
                            <img class="card-img-top" src="https://images.unsplash.com/photo-1497339100210-9e87df79c218?w=1350" alt="Card image cap">
                            <div class="card-body">
                              <h4 class="card-title">特工西裝</h4>
                              <p class="card-text">This is a longer card with supporting text below as a natural lead-in to additional content. This content
                                is a little bit longer.</p>
                            </div>
                            <div class="card-footer border-top-0 bg-white">
                              <a href="#" class="btn btn-outline-secondary btn-block btn-sm">
                                <i class="fa fa-cart-plus" aria-hidden="true"></i> 搶購去
                              </a>
                            </div>
                          </div>
                        </div>

                        <div class="col-md-4 mb-4">
                          <div class="card border-0 box-shadow text-center h-100">
                            <img class="card-img-top" src="https://images.unsplash.com/photo-1485373650022-3ed53f62b8f3?w=634" alt="Card image cap">
                            <div class="card-body">
                              <h4 class="card-title">變聲領帶</h4>
                              <p class="card-text">This is a longer card with supporting text below as a natural lead-in to additional content. This content
                                is a little bit longer.</p>
                            </div>
                            <div class="card-footer border-top-0 bg-white">
                              <a href="#" class="btn btn-outline-secondary btn-block btn-sm disabled">
                                缺貨中
                              </a>
                            </div>
                          </div>
                        </div>
                      </div>
                      <!-- pagination -->
                      <nav aria-label="Page navigation" class="my-5">
                        <ul class="pagination justify-content-center">
                          <li class="page-item disabled">
                            <a class="page-link" href="#" tabindex="-1">Previous</a>
                          </li>
                          <li class="page-item">
                            <a class="page-link" href="#">1</a>
                          </li>
                          <li class="page-item">
                            <a class="page-link" href="#">2</a>
                          </li>
                          <li class="page-item">
                            <a class="page-link" href="#">3</a>
                          </li>
                          <li class="page-item">
                            <a class="page-link" href="#">Next</a>
                          </li>
                        </ul>
                      </nav>
                    </div>

                    <div class="tab-pane" id="list-gift">
                      <div class="row align-items-stretch">
                        <!-- 禮品 -->
                        <div class="col-md-4 mb-4">
                          <div class="card border-0 box-shadow text-center h-100">
                            <img class="card-img-top" src="https://images.unsplash.com/photo-1482173074468-5b323335debe?w=1350" alt="Card image cap">
                            <div class="card-body">
                              <h4 class="card-title">超精緻禮物</h4>
                              <p class="card-text">This is a longer card with supporting text below as a natural lead-in to additional content. This content
                                is a little bit longer.</p>
                            </div>
                            <div class="card-footer border-top-0 bg-white">
                              <a href="#" class="btn btn-outline-secondary btn-block btn-sm">
                                <i class="fa fa-cart-plus" aria-hidden="true"></i> 搶購去
                              </a>
                            </div>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                  <!-- tab-content end -->

                </div>

              </div>
            </div>
            <footer class="bg-light text-muted py-5">
              <div class="container">
                <ul class="list-inline text-center">
                  <li class="list-inline-item">© Copright 2017 六角血拼賣賣</li>
                  <li class="list-inline-item">
                    <a class="text-info" href="#">
                      <i class="fa fa-instagram" aria-hidden="true"></i> Instagrame</a>
                  </li>
                  <li class="list-inline-item">
                    <a class="text-info" href="#">
                      <i class="fa fa-facebook-square" aria-hidden="true"></i> Facebook</a>
                  </li>
                  <li class="list-inline-item">
                    <a class="text-info" href="#">About</a>
                  </li>
                </ul>
                <p class="text-center">Made with Bootstrap4</p>
              </div>
            </footer>

            <div class="modal fade" id="removeModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
              <div class="modal-dialog" role="document">
                <div class="modal-content">
                  <div class="modal-header bg-danger text-white">
                    <h5 class="modal-title">刪除商品</h5>
                    <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                      <span aria-hidden="true">&times;</span>
                    </button>
                  </div>
                  <div class="modal-body">
                    <p>是否確認刪除商品</p>
                  </div>
                  <div class="modal-footer">
                    <button type="button" class="btn btn-outline-secondary" data-dismiss="modal">否</button>
                    <button type="button" class="btn btn-outline-danger px-5">是</button>
                  </div>
                </div>
              </div>
            </div>
      </body>

    </div>
  </template>
  
  

  
  <script type="application/javascript">

import $ from 'jquery'; //載入modal

export default {
  mounted(){
      $(document).ready(function () {
      $('#removeModal').on('show.bs.modal', function (event) {
        var button = $(event.relatedTarget) // 選則當初觸發事件的按鈕
        var title = button.data('title') // 使用 data-* 來取得特定內容

        var modal = $(this)
        modal.find('.modal-title').text('確認' + title) // 寫入資料
      })
    });
  },
  data() {
    return {
      products: [],
      product: {}, //存放查看更多的Modal資料
      isLoading: false,
      status: {
        loadingItem: '', //存放產品id
      },
      cart: {},
      form: { //結構直接參考api設定的資料結構 存放顧客填寫的個人資料
        user: {
          name: '',
          email: '',
          tel: '',
          address: '',
        },
        message: ''
      }
    }
  },
  methods: {
    getProducts() {
      const vm = this;
      const url = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/products/all`;
      vm.isLoading = true;
      this.$http.get(url).then((response) => {
        vm.products = response.data.products;
        console.log(response);
        vm.isLoading = false;
      });
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
    deleteCart(id){
      const vm = this;
      const url = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/cart/${id}`;
      // vm.isLoading = true;
      this.$http.delete(url).then((response) => {
         vm.getCart(); //這部我會忘記做 >> 刪除後重新取得購物車
        console.log(response);
        // vm.isLoading = false;
    });
    },
    createOrder(){ //到上方綁定 >> @submit.prevent="createOrder"
      const vm = this;
      const url = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/order`;
      const order = vm.form; //這部會忘記做
      // vm.isLoading = true;
      this.$validator.validate().then((result)=>{
        if (result){
            this.$http.post(url,{data:order}).then((response) => {
            // vm.getCart(); 
            console.log('訂單已建立',response);
            // vm.isLoading = false;
          })
          }
          else{
            console.log('欄位不完整');
          }
      
      
    });
    },
  },
  created() { //取得資料要在這邊設定
    this.getProducts();
    this.getCart(); //把購物車取得回來
  },
};


  // export default {
  //   mounted(){
  //     $(document).ready(function () {
  //     $('#removeModal').on('show.bs.modal', function (event) {
  //       var button = $(event.relatedTarget) // 選則當初觸發事件的按鈕
  //       var title = button.data('title') // 使用 data-* 來取得特定內容

  //       var modal = $(this)
  //       modal.find('.modal-title').text('確認' + title) // 寫入資料
  //     })
  //   });
  //   }
  // }

     
  </script>





