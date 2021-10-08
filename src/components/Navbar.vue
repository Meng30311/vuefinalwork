<template>
  <div id="top">
    <div class="modal fade" id="loginModal">
      <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">登入</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <div class="loginIcons">
              <a class="btn btn-dark btn-social mx-3 twitter" href="#!"><i class="fab fa-twitter"></i></a>
              <a class="btn btn-dark btn-social mx-3 facebook" href="#!"><i class="fab fa-facebook-f"></i></a>
              <a class="btn btn-dark btn-social mx-3 linkedin" href="#!"><i class="fab fa-linkedin-in"></i></a>
            </div>
            <div class="loginInfo">
              <input type="email" placeholder="Email" v-model="user.username">
              <input type="password" placeholder="Password" v-model="user.password">
            </div>
            <div class="loginBtn">
              <button @click="login()">登入</button>
            </div>
          </div>
        </div>
      </div>
    </div>
    <nav class="navbar navbar-expand-lg navbar-dark fixed-top" id="mainNav">
      <div class="container">
        <router-link class="navbar-brand js-scroll-trigger logo" to="/"></router-link>
        <button class="navbar-toggler navbar-toggler-right" type="button" data-toggle="collapse"
          data-target="#navbarResponsive" aria-controls="navbarResponsive" aria-expanded="false"
          aria-label="Toggle navigation">
          Menu
          <i class="fas fa-bars ml-1"></i>
        </button>
        <div class="collapse navbar-collapse" id="navbarResponsive">
          <ul class="navbar-nav text-uppercase ml-auto">
            <li class="nav-item">
              <router-link class="nav-link js-scroll-trigger" to="/products">商品列表</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link js-scroll-trigger" to="/customerorder">我的訂單</router-link>
            </li>
            <li class="nav-item" v-if="!isLogin">
              <a href="#" class="nav-link" data-toggle="modal" data-target="#loginModal">登入</a>
            </li>
            <li class="nav-item" v-if="isLogin">
              <a href="#" class="nav-link" @click.prevent="logout()">登出</a>
            </li>
            <li class="nav-item">
              <div class="dropdown">
                <a class="nav-link js-scroll-trigger dropdown-toggle" role="button" data-toggle="dropdown" href="#">
                  <span class="fa-1x position-relative">
                    <i class="fas fa-cart-plus"></i>
                    <span class="badge badge-pill badge-danger">{{cart.carts.length}}</span>
                  </span>
                </a>
                <div class="dropdown-menu" aria-labelledby="dropdownMenuButton">
                  <div class="px-3 py-2">
                    <p>已選擇商品</p>
                    <table class="table table-sm" v-if="cart.carts.length >= 1">
                      <tr v-for="item in cart.carts" :key="item.id">
                        <td>
                          <a href="#" @click.prevent="delCart(item.id)">
                            <i class="far fa-trash-alt"></i>
                          </a>
                        </td>
                        <td>{{item.product.title}}</td>
                        <td>{{item.qty}}晚</td>
                        <td class="text-right">${{item.total}}</td>
                      </tr>
                      <tr>
                        <td colspan="3" class="text-right">總計</td>
                        <td class="text-right">${{cart.total}}</td>
                      </tr>
                    </table>
                    <a href="#" class="btn btn-primary w-100" v-if="cart.carts.length >= 1">
                      <span>
                        <i class="fas fa-cart-arrow-down" aria-hidden="true"></i>
                      </span>
                      結帳去
                    </a>
                    <div v-if="cart.carts.length === 0" class="">
                      <p class="text-center">購物車是空的</p>
                      <div class="w-100 d-flex">
                        <router-link to="/products" class="btn btn-primary mx-auto"><span class="mr-2"><i
                              class="fas fa-cart-plus"></i></span>購物去</router-link>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </li>
          </ul>
        </div>
      </div>
    </nav>
    <Alert />
  </div>
</template>

<script>
  import Alert from '@/components/Alert'
  import $ from 'jquery'

  export default {
    components: {
      Alert,
    },
    data() {
      return {
        cart: {
          carts:{}
        },
        user:{
          username:'',
          password:''
        },
        isLogin:false,
      }
    },
    methods: {
      getCart(){
        const api = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/cart`;
        const vm = this;
        this.$http.get(api).then(response => {
          vm.cart = response.data.data;
          vm.$bus.$emit('getCart');
        });
      },
      delCart(id) {
        const api = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/cart/${id}`;
        const vm = this;
        this.$http.delete(api).then(response => {
          if (response.data.success) {
            vm.getCart();
            vm.$bus.$emit('message:push', '刪除成功', 'danger');
          };
        });
        $('.dropdown-toggle').dropdown("hide");
      },
      login() {
        const api = `${process.env.APIPATH}/admin/signin`;
        const vm=this;
        this.$http.post(api,vm.user).then(response => {
          if (response.data.success) {
            $('#loginModal').modal('hide');
            vm.isLogin=true;
          }else{
            alert('登入失敗');
            $('#loginModal').modal('hide');
          };
        });
      },
      logout(){
        const api = `${process.env.APIPATH}/logout`;
        const vm=this;
        this.$http.post(api).then(response => {
          alert('已登出');
          vm.isLogin=false;
        });
      },
    },
    created(){
      const vm = this;
      this.getCart();
      vm.$bus.$on('getCartInfo', () => {
        vm.getCart();
      });
      vm.$bus.$on('isLogin', isLogin => {
        vm.isLogin=isLogin;
      });
    },
    mounted() {
      document.addEventListener('scroll', function () {
        if ($("#mainNav").offset().top > 100) {
          $("#mainNav").addClass("navbar-shrink");
        } else {
          $("#mainNav").removeClass("navbar-shrink");
        };
      });
    },
  }

</script>

<style scoped>
  .badge {
    font-size: 5px;
    position: absolute;
    bottom: -2px;
    right: -8px
  }

  .dropdown-toggle::after {
    display: none;
  }

  .dropdown-menu {
    min-width: 300px;
    z-index: 9999;
    left: 10px;
    top: 45px;
  }

  td a {
    font-size: 18px
  }

  .container {
    width: 1340px;
  }
  .modal-content{
    width:100%;
  }
  .modal-header{
    justify-content:center;
    border-bottom:0;
  }
  .modal-header h5{
    margin-left:209px;
  }
  .modal-title{
    font-size:25px;
    font-weight:bold;
  }
  .twitter{
      background-color:rgba(29, 161, 242);
      border-color:rgba(29 ,161, 242);
  }
  .facebook{
      background-color:rgba(66,102,179);
      border-color:rgba(66,102,179);
  }
  .linkedin{
      background-color:rgba(14,118,168);
      border-color:rgba(14,118,168);
  }
  .loginIcons{
    display:flex;
    justify-content:center;
  }
  .loginInfo{
    margin-top:20px;
    display:flex;
    flex-direction:column;
    align-items:center;
  }
  .loginInfo input{
    width:75%;
    padding:12px 15px;
    background-color:#eee;
    border:none;
    margin:8px 0;
    border-radius:10px;
  }
  .loginBtn{
    display:flex;
    justify-content:center;
    margin-top:10px;
  }
  .loginBtn button{
    border-radius:20px;
    border:1px solid #ff4b2b;
    background-color:#ff4b2b;
    color:white;
    font-size:16px;
    font-weight:bold;
    padding:12px 40px;
    letter-spacing:1px;
  }
</style>
