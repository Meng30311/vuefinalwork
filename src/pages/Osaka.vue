<template>
  <div>
    <loading :active.sync="isLoading">
      <img src="@/assets/img/loading.png" class="ld ld-dim" width="400">
    </loading>
    <header class="proHeader"
      style="background-image: url(https://gsimg.asiayo.com/ay-image-upload/1513154824683_1492065219937_Osaka_city_yvonne.jpg);">
      <div class="container">
        <h3 class="masthead-subheading h1">大阪自由行｜大阪旅遊景點</h3>
        <div class="masthead-heading text-uppercase mt-3">大阪旅遊景點及住宿</div>
      </div>
    </header>
    <div class="container mt-5 mb-3">
      <h5>推薦景點</h5>
      <hr height="2">
      <div class="carousel slide" id="carouselExampleControls" data-ride="carousel">
        <div class="carousel-inner">
          <div class="carousel-item active">
            <div class="row mt-4">
              <div class="col-md-4">
                <div class="card">
                  <div class="card-img-top">
                    <img src="https://resources.matcha-jp.com/resize/720x2000/2019/08/02-82968.jpeg" class="card-img-top" ref="osakasrc1">
                  </div>
                  <div class="card-body">
                    <h4 class="card-title">
                      <span class="icon"><i class="fas fa-map-marker-alt"></i></span>
                      <span class="ml-2" ref="osakatitle1">道頓崛 心齋橋</span>
                    </h4>
                    <p class="card-text" ref="osakatext1">道頓崛、心齋橋可以說是大阪最熱鬧的區域，幾乎是人人到大阪旅遊都會去的地方。</p>
                    <a href="#modal" data-toggle="modal" class="btn btn-outline-primary" @click="modalInfo(id=0)">詳細介紹</a>
                  </div>
                </div>
              </div>
              <div class="col-md-4" v-for="item in products" v-if="item.category === '道頓崛'" :key="item.id">
                <div class="card">
                  <div class="card-img-top"
                    :style="{backgroundImage:`url(${item.imageUrl})`}">
                  </div>
                  <div class="card-body">
                    <h4 class="card-title">
                      <span class="icon"><i class="fas fa-bed"></i></span>
                      <span class="ml-2">{{item.title}}</span>
                    </h4>
                    <p class="card-text">{{item.description}}</p>
                    <div class="d-flex justify-content-between">
                      <a href="#" class="btn btn-outline-primary" @click.prevent="getSingle(item.id)">
                        <template v-if="loadingStatus.modalLoading & loadingStatus.loadingItem === item.id">
                          <span class="mr-2">
                            <i class="fas fa-spinner fa-spin"></i>
                          </span>
                        </template>
                        <template v-else>
                          <span class="mr-2"><i class="fas fa-search-plus"></i>
                          </span>
                        </template>
                        查看更多
                      </a>
                      <a href="#" class="btn btn-outline-primary" @click.prevent="addCart(item.id)">
                        <template v-if="loadingStatus.isCart & loadingStatus.loadingItem === item.id">
                          <span class="mr-2">
                            <i class="fas fa-spinner fa-spin"></i>
                          </span>
                        </template>
                        <template v-else>
                          <span class="mr-2"><i class="fas fa-cart-plus"></i>
                          </span>
                        </template>
                        加入購物車
                      </a>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div class="row mt-4">
              <div class="col-md-4">
                <div class="card">
                  <div class="card-img-top">
                    <img src="https://youimg1.tripcdn.com/target/100o1f000001gp35uEFD5_C_750_500.jpg?proc=source%2Ftrip" class="card-img-top" ref="osakasrc2">
                  </div>
                  <div class="card-body">
                    <h4 class="card-title">
                      <span class="icon"><i class="fas fa-map-marker-alt"></i></span>
                      <span class="ml-2" ref="osakatitle2">通天閣</span>
                    </h4>
                    <p class="card-text" ref="osakatext2">通天閣被稱為浪速的艾菲爾鐵塔，原因在於基座是模仿凱旋門，塔身是參考艾菲爾鐵塔。</p>
                    <a href="#modal" data-toggle="modal" class="btn btn-outline-primary" @click="modalInfo(id=1)">詳細介紹</a>
                  </div>
                </div>
              </div>
              <div class="col-md-4" v-for="item in products" v-if="item.category === '通天閣'" :key="item.id">
                <div class="card">
                  <div class="card-img-top"
                    :style="{backgroundImage:`url(${item.imageUrl})`}">
                  </div>
                  <div class="card-body">
                    <h4 class="card-title">
                      <span class="icon"><i class="fas fa-bed"></i></span>
                      <span class="ml-2">{{item.title}}</span>
                    </h4>
                    <p class="card-text">{{item.description}}</p>
                    <div class="d-flex justify-content-between">
                      <a href="#" class="btn btn-outline-primary" @click.prevent="getSingle(item.id)">
                        <template v-if="loadingStatus.modalLoading & loadingStatus.loadingItem === item.id">
                          <span class="mr-2">
                            <i class="fas fa-spinner fa-spin"></i>
                          </span>
                        </template>
                        <template v-else>
                          <span class="mr-2"><i class="fas fa-search-plus"></i>
                          </span>
                        </template> 查看更多
                      </a>
                      <a href="#" class="btn btn-outline-primary" @click.prevent="addCart(item.id)">
                        <template v-if="loadingStatus.isCart & loadingStatus.loadingItem === item.id">
                          <span class="mr-2">
                            <i class="fas fa-spinner fa-spin"></i>
                          </span>
                        </template>
                        <template v-else>
                          <span class="mr-2"><i class="fas fa-cart-plus"></i>
                          </span>
                        </template> 加入購物車
                      </a>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="carousel-item">
            <div class="row mt-4">
              <div class="col-md-4">
                <div class="card">
                  <div class="card-img-top">
                    <img src="https://blog.asiayo.com/wp-content/uploads/1510742348253_universal-studios-1640516_960_720.jpg" class="card-img-top" ref="osakasrc3">
                  </div>
                  <div class="card-body">
                    <h4 class="card-title">
                      <span class="icon"><i class="fas fa-map-marker-alt"></i></span>
                      <span class="ml-2" ref="osakatitle3">環球影城</span>
                    </h4>
                    <p class="card-text" ref="osakatext3">全球共有 4 個環球影城，其中一個就在大阪，最熱門的區域非哈利波特區莫屬。</p>
                    <a href="#modal"  data-toggle="modal" class="btn btn-outline-primary" @click="modalInfo(id=2)">詳細介紹</a>
                  </div>
                </div>
              </div>
              <div class="col-md-4" v-for="item in products" v-if="item.category === '環球'" :key="item.id">
                <div class="card">
                  <div class="card-img-top"
                    :style="{backgroundImage:`url(${item.imageUrl})`}">
                  </div>
                  <div class="card-body">
                    <h4 class="card-title">
                      <span class="icon"><i class="fas fa-bed"></i></span>
                      <span class="ml-2">{{item.title}}</span>
                    </h4>
                    <p class="card-text">{{item.description}}</p>
                    <div class="d-flex justify-content-between">
                      <a href="#" class="btn btn-outline-primary" @click.prevent="getSingle(item.id)">
                        <template v-if="loadingStatus.modalLoading & loadingStatus.loadingItem === item.id">
                          <span class="mr-2">
                            <i class="fas fa-spinner fa-spin"></i>
                          </span>
                        </template>
                        <template v-else>
                          <span class="mr-2"><i class="fas fa-search-plus"></i>
                          </span>
                        </template> 查看更多
                      </a>
                      <a href="#" class="btn btn-outline-primary" @click.prevent="addCart(item.id)">
                        <template v-if="loadingStatus.isCart & loadingStatus.loadingItem === item.id">
                          <span class="mr-2">
                            <i class="fas fa-spinner fa-spin"></i>
                          </span>
                        </template>
                        <template v-else>
                          <span class="mr-2"><i class="fas fa-cart-plus"></i>
                          </span>
                        </template> 加入購物車
                      </a>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div class="row mt-4">
              <div class="col-md-4">
                <div class="card">
                  <div class="card-img-top">
                    <img src="https://859100.smushcdn.com/1882524/wp-content/uploads/2016/12/%E5%A4%A7%E9%98%AA%E5%9F%8E.jpg?lossy=0&strip=1&webp=1" class="card-img-top" ref="osakasrc4">
                  </div>
                  <div class="card-body">
                    <h4 class="card-title">
                      <span class="icon"><i class="fas fa-map-marker-alt"></i></span>
                      <span class="ml-2" ref="osakatitle4">大阪城</span>
                    </h4>
                    <p class="card-text" ref="osakatext4">跟名古屋、熊本城並列日本三大名城，頂端的展望台可以俯瞰大阪風景。</p>
                    <a href="#modal" data-toggle="modal" class="btn btn-outline-primary" @click="modalInfo(id=3)">詳細介紹</a>
                  </div>
                </div>
              </div>
              <div class="col-md-4" v-for="item in products" v-if="item.category === '大阪城'" :key="item.id">
                <div class="card">
                  <div class="card-img-top"
                    :style="{backgroundImage:`url(${item.imageUrl})`}">
                  </div>
                  <div class="card-body">
                    <h4 class="card-title">
                      <span class="icon"><i class="fas fa-bed"></i></span>
                      <span class="ml-2">{{item.title}}</span>
                    </h4>
                    <p class="card-text">{{item.description}}</p>
                    <div class="d-flex justify-content-between">
                      <a href="#" class="btn btn-outline-primary" @click.prevent="getSingle(item.id)">
                        <template v-if="loadingStatus.modalLoading & loadingStatus.loadingItem === item.id">
                          <span class="mr-2">
                            <i class="fas fa-spinner fa-spin"></i>
                          </span>
                        </template>
                        <template v-else>
                          <span class="mr-2"><i class="fas fa-search-plus"></i>
                          </span>
                        </template> 查看更多
                      </a>
                      <a href="#" class="btn btn-outline-primary" @click.prevent="addCart(item.id)">
                        <template v-if="loadingStatus.isCart & loadingStatus.loadingItem === item.id">
                          <span class="mr-2">
                            <i class="fas fa-spinner fa-spin"></i>
                          </span>
                        </template>
                        <template v-else>
                          <span class="mr-2"><i class="fas fa-cart-plus"></i></span>
                        </template> 加入購物車
                      </a>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <a class="carousel-control-prev" href="#carouselExampleControls" role="button" data-slide="prev">
          <span class="carousel-control-prev-icon" aria-hidden="true">
            <i class="fas fa-angle-left"></i>
          </span>
          <span class="sr-only">Previous</span>
        </a>
         <a class="carousel-control-next" href="#carouselExampleControls" role="button" data-slide="next">
          <span class="carousel-control-next-icon" aria-hidden="true">
            <i class="fas fa-angle-right"></i>
          </span>
          <span class="sr-only">Next</span>
        </a>
      </div>
    </div>
    <Footer/>
    <Modal/>
    <Alert/>
  </div>
</template>

<script>
 import Modal from '@/components/Modal'
 import Alert from '@/components/Alert'
 import Footer from '@/components/Footer'
 import $ from 'jquery'

 export default{
   components: {
      Modal,
      Alert,
      Footer,
   },
   data(){
     return{
       modal: {
          title: [],
          src: [],
          text: [],
       },
       emitInfo: {
          modalSrc: '',
          modalTitle: '',
          modalText: '',
       },
       singleProduct:{
          origin_price:'',
          price:'',
          id:'',
          qty:1,
       },
       loadingStatus:{
         loadingItem:'',
         modalLoading:false,
         isCart:false,
       },
       products:{},
       ref: {},
       isLoading:false,
       cart:{},
     }
   },
   methods:{
     modalInfo(id){
       const vm=this;
       this.modal.src=[vm.ref.osakasrc1.src,vm.ref.osakasrc2.src,vm.ref.osakasrc3.src,vm.ref.osakasrc4.src];
       this.modal.title=[vm.ref.osakatitle1.innerHTML,vm.ref.osakatitle2.innerHTML,vm.ref.osakatitle3.innerHTML,vm.ref.osakatitle4.innerHTML];
       this.modal.text=[vm.ref.osakatext1.innerHTML,vm.ref.osakatext2.innerHTML,vm.ref.osakatext3.innerHTML,vm.ref.osakatext4.innerHTML];
       
       this.emitInfo.modalSrc = vm.modal.src[id];
       this.emitInfo.modalText = vm.modal.text[id];
       this.emitInfo.modalTitle = vm.modal.title[id];
       this.$bus.$emit('modalinfo', vm.emitInfo,vm.singleProduct);
     },
     getProducts() {
        const api = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/products/all`;
        const vm = this;
        this.isLoading = true;
        this.$http.get(api).then(response => {
          vm.products = response.data.products;
          vm.isLoading = false;
        });
     },
     getSingle(id) {
        const api = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/product/${id}`;
        const vm = this;
        this.loadingStatus.loadingItem = id;
        this.loadingStatus.modalLoading = true;
        this.$http.get(api).then(response => {
          vm.emitInfo.modalSrc = response.data.product.imageUrl;
          vm.emitInfo.modalText = response.data.product.description;
          vm.emitInfo.modalTitle = response.data.product.title;
          vm.singleProduct.origin_price = response.data.product.origin_price;
          vm.singleProduct.price = response.data.product.price;
          vm.singleProduct.id = response.data.product.id;
          vm.$bus.$emit('modalinfo', vm.emitInfo, vm.singleProduct, true);
          vm.loadingStatus.modalLoading = false;
          $('#modal').modal('show');
          vm.loadingStatus.loadingItem = '';
        });
     },
     addCart(id, qty = 1) {
        const api = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/cart`;
        const vm = this;
        const cart = {
          product_id: id,
          qty,
        };
        this.loadingStatus.loadingItem = id;
        this.loadingStatus.isCart = true;
        this.$http.post(api, {
          data: cart
        }).then(response => {
          vm.$bus.$emit('loadingOver', false);
          vm.loadingStatus.loadingItem = '';
          vm.loadingStatus.isCart = false;
          $('#modal').modal('hide');
          vm.getCart();
          vm.$bus.$emit('message:push', '新增成功', 'success');
        });
     },
     getCart(){
        const api = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/cart`;
        const vm = this;
        this.$http.get(api).then(response => {
          vm.isLoading = false;
          vm.cart = response.data.data;
          vm.$bus.$emit('getCartInfo', vm.cart);
        });
     },
   },
   created(){
     const vm=this;
     this.getProducts();
   },
   mounted(){
     const vm = this;
     this.ref = vm.$refs;
     $('#carouselExampleControls').carousel('pause');
   },
 }
</script>

<style scoped>
  .proHeader {
    height: 400px;
    background-position: center;
    background-size: cover;
    text-align: center;
    color: white;
    text-shadow: 0 2px 4px rgba(0, 0, 0, 0.5);
    display: flex;
    align-items: center;
  }

  .masthead-heading {
    font-size: 20px;
    text-shadow: 0 2px 4px rgba(0, 0, 0, 0.5);
    font-weight: bold;
  }
  .carousel{
    width:auto;
  }
  .card-img-top {
    height: 300px;
    background-position: center;
    background-size: cover;
  }
  .icon {
    color: rgba(52, 152, 219, 0.8);
  }
  .card {
    height: 100%;
  }
  .card-text {
    height: 84px;
  }
  .carousel-control-prev{
    left:-180px;
  }
  .carousel-control-next{
    right:-180px;
  }
  .carousel-control-prev-icon{
    color:black;
    font-size:30px;
  }
  .carousel-control-next-icon{
    color:black;
    font-size:30px;
  }
</style>
