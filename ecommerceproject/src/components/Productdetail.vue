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
                <button class="btn btn-sm btn-cart" data-toggle="dropdown" data-flip="false">
                    <i class="fa fa-shopping-cart text-dark fa-2x" aria-hidden="true"></i>
                    <span class="badge badge-pill badge-danger" v-for="item in cart.carts">{{ item.qty }}</span>
                    <span class="sr-only">unread messages</span>
                </button>
                <div class="dropdown-menu dropdown-menu-right p-3" style="min-width: 300px" data-offset="400">
                    <h6>已選擇商品</h6>
                    <table class="table table-sm">
                    <tbody>
                        <tr v-for="item in cart.carts">
                        <td class="align-middle text-center">
                            <button type="button" class="btn btn-outline-danger btn-sm" @click="deleteCart(item.id)">
                            <i class="fa fa-trash-o" aria-hidden="true"></i>
                            </a>
                            </button>
                        </td>
                        <td class="align-middle">
                            {{ item.product.title }}
                            <!-- <div class="text-success" v-if="item.coupon">
                            已套用優惠券
                            </div> -->
                        </td>
                        <td class="align-middle">{{ item.qty }}/{{ item.product.unit }}</td>
                        <td class="align-middle text-right">{{ item.final_total }}</td>
                        </tr>
                    </tbody>
                    <tfoot>
                        <tr>
                        <td colspan="3" class="text-right">總計</td>
                        <td class="text-right">{{ cart.total }}</td>
                        </tr>
                    </tfoot>
                    </table>
                    <router-link to="/checkout" class="btn btn-primary btn-block">
                    <i class="fa fa-cart-plus" aria-hidden="true"></i> 結帳去
                    </router-link>
                </div>
                
            </nav>
            <div class="container main-contant mb-1">
                <nav aria-label="breadcrumb" role="navigation">
                <ol class="breadcrumb bg-transparent pl-0">
                    <li class="breadcrumb-item">
                    <router-link to="/home">首頁</router-link>
                    </li>
                    <li class="breadcrumb-item">
                    <a href="#" v-if="item.category==='工作坊'">{{item.category}}</a>
                    </li>
                    <li class="breadcrumb-item active" aria-current="page" >0.0.0</li>
                </ol>
                </nav>
                <div class="row">
                <div class="col-md-4 mb-5">
                    <div class="sticky-top" style="top: 10px;">
                    <h1 class="h2">金牌西裝
                        <small class="text-muted">(加拉哈德版)</small>
                    </h1>
                    <div class="d-flex my-3 align-items-end justify-content-end">
                        <del class="text-muted">售價 $1299</del>
                        <div class="h3 mb-0 ml-auto text-danger">
                        <small>網路價 NT$</small>
                        <strong>520</strong>
                        </div>
                    </div>
                    

                    <div class="input-group mt-3">
                        <select name="" class="form-control mr-1" id="" v-model="product.num">
                            <option :value="num" v-for="num in 10" :key="num">
                                選購{{num}} {{product.unit}}
                            </option>
                        </select>
                        <a class="btn btn-primary" @click="addtoCart(product.id, product.num)">
                        <i class="fas fa-spinner fa-spin"  v-if="status.loadingItem === product.id"></i>
                         加入購物車
                        </a>
                    </div>

                    <div class="mt-2 text-right text-muted">
                        <i class="fa fa-cc-visa" aria-hidden="true"></i>
                        <i class="fa fa-cc-jcb" aria-hidden="true"></i>
                        <i class="fa fa-cc-paypal" aria-hidden="true"></i>
                    </div>

                    </div>


                </div>
                <div class="col-md-8">
                    <h2 v-for="item in cart.carts">{{ item.product.description }}</h2>
                    <p class="card-text">This is a longer card with supporting text below as a natural lead-in to additional content. This content is a little
                    bit longer.</p>

                    <h3 class="mt-5 text-center">合身剪裁</h3>
                    <img src="https://images.unsplash.com/photo-1472417583565-62e7bdeda490?w=634" class="w-100" alt="">

                    <h3 class="mt-5 text-center">簡單就好</h3>
                    <img src="https://images.unsplash.com/photo-1497339100210-9e87df79c218?w=1500" class="w-100" alt="">

                    <h3 class="mt-5 text-center">不佔空間</h3>
                    <img src="https://images.unsplash.com/photo-1475530060488-75a6de1dca6f?w=675" class="w-100" alt="">
                    <div class="alert alert-secondary mt-4" role="alert">
                    <h2 class="text-center">購物說明</h2>
                    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Veniam, at! Totam, exercitationem repellat. Saepe facere
                        amet expedita perferendis voluptatem dicta dignissimos tempora ut atque, rerum doloribus? Magni, blanditiis.
                        Assumenda, distinctio!</p>
                    </div>
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


<script>

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
                        vm.isLoading = true;
                        vm.status.loadingItem = id;
                        this.$http.get(url).then((response) => {
                            vm.product = response.data.product; //先讀取完資料後
                            $('#productModal').modal('show'); //再將Modal打開
                            console.log(response);
                            vm.isLoading = false;  
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
                        vm.isLoading = true;
                        this.$http.delete(url).then((response) => {
                            vm.getCart(); //這部我會忘記做 >> 刪除後重新取得購物車
                            console.log(response);
                            vm.isLoading = false;
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
                    mounted(){
                        $(document).ready(function () {
                            $('#removeModal').on('show.bs.modal', function (event) {
                                var button = $(event.relatedTarget) // 選則當初觸發事件的按鈕
                                var title = button.data('title') // 使用 data-* 來取得特定內容

                                var modal = $(this)
                                modal.find('.modal-title').text('確認' + title) // 寫入資料
                            })
                        });
                    }
                }
</script>