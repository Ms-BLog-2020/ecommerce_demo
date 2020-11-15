<html>
  <div>
    <div class="hello">
      <a href="#" @click.prevent="signout">登出</a>
    </div>
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
    
  </div>



  <script>
  export default {
    name: 'HelloWorld',
    data () {
      return {
        msg: 'Welcome to Your Vue.js App'
      }
    },
    methods: {
      signout(){
          const api = `${process.env.APIPATH}/logout`; 
          const vm = this;
          this.$http.post(api).then((response) => { //post>>把用戶的資料傳進來
          console.log(response.data);
          if (response.data.success){
              vm.$router.push('/login');
          }
        });
      }
    }
  }
  </script>


</html>



