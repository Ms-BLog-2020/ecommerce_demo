<template>
    <div>
        <form>
                <h4 class="text-center my-4">購買資訊</h4>
                <table class="table table-sm">
                <thead>
                    <tr>
                    <th width="100"></th>
                    <th>商品名稱</th>
                    <th width="100">數量</th>
                    <th width="80">小計</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                    
                    <td class="align-middle"></td>
                    <td class="align-middle"></td>
                    <td class="align-middle"></td>
                    <td class="align-middle text-right">$520</td>
                    </tr>
                    <tr>
                    <td colspan="3" class="text-right">合計</td>
                    <td class="text-right">
                        <strong>$580</strong>
                    </td>
                    </tr>
                </tbody>
                </table>
                <hr>
                <h4 class="text-center my-4">個人資料</h4>
                <table class="table">
                <tbody>
                    <tr>
                    <th width="200">Email</th>
                    <td></td>
                    </tr>
                    <tr>
                    <th>姓名 </th>
                    <td></td>
                    </tr>
                    <tr>
                    <th>電話 </th>
                    <td></td>
                    </tr>
                    <tr>
                    <th>地址 </th>
                    <td></td>
                    </tr>
                </tbody>
                </table>
                
            </form>
    </div>
</template>

<script>
export default {
    data(){
        return{
          orderId: '',
          order: {}
        }
    },
    methods:{
        finishOrder(){
            const vm = this;
            const url = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/admin/orders/${vm.orderId}`;
            // vm.isLoading = true;
            this.$http.get(url).then((response) => {
                vm.order= response.data.order;
                console.log(response);
                // vm.isLoading = false;
        });
        },
        // payOrder(){
        //     const vm = this;
        //     const url = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/pay/${vm.orderId}`;
        //     vm.isLoading = true;
        //     this.$http.post(url).then((response) => {
        //         console.log(response);
        //         if (response.data.success){
        //             vm.getOrder();
        //         }
        // //         vm.isLoading = false;
        // });
        // }
    },
    created(){
       this.orderId=this.$route.params.orderId;
        console.log(this.orderId);
        this.finishOrder();
        
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