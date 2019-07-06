<template>
  <v-app>
    <v-navigation-drawer fixed :temporary="$vuetify.breakpoint.mdAndUp" app v-model="drawer">
      <v-list dense>
        <template v-for="item in items"  >
          <v-list-group v-if="item.children" v-model="item.model" :key="item.text" :prepend-icon="item.model ? item.icon : item['icon-alt']" append-icon="">
            <v-list-tile slot="activator">
              <v-list-tile-content>
                <v-list-tile-title>
                  {{ item.text }}
                </v-list-tile-title>
              </v-list-tile-content>
            </v-list-tile>
            <v-list-tile v-for="(child, i) in item.children" :key="i" >
              <v-list-tile-action v-if="child.icon">
                <v-icon>{{ child.icon }}</v-icon>
              </v-list-tile-action>
              <v-list-tile-content>
                <v-list-tile-title>
                  {{ child.text }}
                </v-list-tile-title>
              </v-list-tile-content>
            </v-list-tile>
          </v-list-group>
          <v-list-tile v-else :key="item.text" router :to="item.route">
            <v-list-tile-action>
              <v-icon>{{ item.icon }}</v-icon>
            </v-list-tile-action>
            <v-list-tile-content>
              <v-list-tile-title>
                {{ item.text }}
              </v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
        </template>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar color="white" app :clipped-left="$vuetify.breakpoint.mdAndUp" fixed >
      <v-toolbar-side-icon @click.stop="drawer = !drawer"></v-toolbar-side-icon>
      <img style="width:150px;" src="./assets/femaledaily.png" >
      <v-spacer></v-spacer>
      <v-toolbar-title style="width: 1024px;"  class="ml-0 pl-0">
        <v-text-field  solo flat label="Search product, articles, topics, brand, etc" prepend-inner-icon="search" style="border:1px solid #e0e0e0;border-radius:3px;" ></v-text-field>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-toolbar-items style="background-color:#db284e;">
        <v-btn flat large dark>
          <v-icon dark left>person_outline</v-icon>LOGIN / SIGNUP
        </v-btn>
      </v-toolbar-items>
      <template v-slot:extension>
        <v-spacer></v-spacer>
          <v-toolbar-title >
            <v-btn flat large light><strong>SKINCARE</strong></v-btn>
            <v-btn flat large light><strong>MAKE UP</strong></v-btn>
            <v-btn flat large light><strong>BODY</strong></v-btn>
            <v-btn flat large light><strong>HAIR</strong></v-btn>
            <v-btn flat large light><strong>FRAGRACE</strong></v-btn>
            <v-btn flat large light><strong>NAILS</strong></v-btn>
            <v-btn flat large light><strong>TOOLS</strong></v-btn>
            <v-btn flat large light><strong>BRANDS</strong></v-btn>
          </v-toolbar-title>
        <v-spacer></v-spacer>
      </template>
    </v-toolbar>
    <v-content style="padding:108px 0px 0px">
      <v-layout align-center justify-center column >
            <v-layout align-center  style="height:50px;width:970px;" class="banner">
              <v-flex text-xs-center class="banner-text">
                <p><strong>TOP FRAME</strong> banner</p>
                <p>970x50 pixel</p>
              </v-flex>
            </v-layout>
            <v-layout align-end column style="width:970px;">
              <v-btn dark color="#db284e"><v-icon>close</v-icon>Close</v-btn>
            </v-layout>
            <v-layout align-center justify-center row reverse fill-height style="height:250px;width:970px;" class="banner">
              <v-flex text-xs-center class="banner-text">
                <p><strong>BILLBOARD</strong> banner</p>
                <p>970x250 pixel</p>
              </v-flex>
            </v-layout>
      </v-layout>
      <v-container align-center justify-center column grid-list-lg>
        <v-layout class="title-card-product">
          <v-flex xs12>
            <h2>
              Editor's Choice
            </h2>
            <p>
              Curated with love
            </p>
          </v-flex>
        </v-layout>
        <v-layout row wrap style="padding-top:40px;">
          <v-flex xs2 v-for="products in product" v-bind:key="products.id">
            <v-card class="elevation-0 black--text">
              <v-btn  absolute top left fab>
              <v-avatar size="60px" :tile="tile">
                  <img src="//static.femaledaily.com/dyn/70/images/user-pics/64e507749ca86ddc63151ed528bec179.jpg" alt="Avatar">
              </v-avatar>
              </v-btn>
              <v-card-text class="title-product">
                <p class="editor-name">{{products.editor}}</p>
                <p class="editor-position">{{products.role}}</p>
              </v-card-text>
              <v-layout>
                <v-flex xs12>
                  <a style="width:140px;height:177px;">
                  <v-img  v-bind:src="products.product['image']" contain ></v-img>
                  </a>
                </v-flex>
              </v-layout>
              <v-card-actions class="pa-2">
                <span class="black--text text--lighten-2 caption ">
                  <h3>{{products.product["rating"]}}</h3>
                </span>
                <v-rating background-color="primary" color="primary accent-4" dense value="4.3" readonly size="18"></v-rating>
                <span class="black--text text--lighten-2 caption mr-2">
                  <strong>(56)</strong>
                </span>
              </v-card-actions>
                    <div>
                      <div class="headline">{{products.product['name']}}</div>
                      <div>{{products.product['description']}}</div>
                    </div>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
        
      <v-jumbotron :gradient="gradient" dark src="https://s3-ap-southeast-1.amazonaws.com/assets.femaledaily.com/web-assets/banner_matches_visitor.png">
        <v-container fill-height>
          <v-layout align-center>
              <v-card-text class="jumbotron-banner">
                <p class="jumbotron-title">Psst! We give product matches that will be perfect for you!</p>
                <p class="jumbotron-desc">They will fit your skin, hair, body, AND they solve your beauty concerns at the same time. Sign up and complete your Beauty ID now!</p>
                <v-btn class="primary" large absolute bottom right style="border-radius:5px;">
                Log In / Sing Up
                </v-btn>
              </v-card-text>
          </v-layout>
        </v-container>
      </v-jumbotron>
      <v-layout style="padding:50px 0 10px 0;" align-center justify-center column >
            <v-layout align-center justify-center row reverse fill-height style="height:250px;width:970px;" class="banner">
              <v-flex text-xs-center class="banner-text">
                <p><strong>BILLBOARD</strong> banner</p>
                <p>970x250 pixel</p>
              </v-flex>
            </v-layout>
      </v-layout>
        <v-container>
    <v-layout row wrap>
          <v-flex xs4 v-for="article in articles" v-bind:key="article.id">
            <v-card class="elevation-0 black--text">
              <v-layout>
                <v-flex xs12>
                  <a >
                  <v-img src="http://imgcdn.femaledaily.com/2019/07/SKINCARE-SEMANGKA-675.jpg"  contain ></v-img>
                  </a>
                </v-flex>
              </v-layout>
                    <div>
                      <div class="headline">Supermodel</div>
                      <div>Foster the People</div>
                      <div>(2014)</div>
                    </div>
            </v-card>
          </v-flex>
          
        </v-layout>
  </v-container>
      
 

      
    </v-content>
    
  </v-app>

</template>

<script>
import axios from 'axios'
export default {
  name: 'App',
  props: ["editor's choice"],
  data (){
    return{
     dialog: false,
      drawer: null,
      items: [{ icon: 'dashboard', text: 'Dashboard', route :'/' },{ icon: 'person', text: 'User', route:'/User' }],
      product: [],
      articles:[]
  }
  },
    mounted () {
    axios
      .get('https://virtserver.swaggerhub.com/hqms/FDN-WP/0.1/wp')
      .then(response => {
        this.product = response.data["editor's choice"];
        this.articles = response.data["latest articles"];

      })
      .catch(error => {
        console.log(error)
      })
  } }

</script>
<style>
  .theme--light.application{
    background: #fff;
  }
  .v-toolbar__content{
    padding-right: 0px;
  }
  .v-text-field.v-text-field--solo .v-input__control{
    min-height:38px;
  }
  .v-input__slot{
    margin:0px;
  }
  .v-toolbar__items .v-btn:not(.v-btn--floating):not(.v-btn--icon){
    padding:10px 36px;
  }
  .v-label{
    font-size:14px;
  }
  .v-toolbar__extension{
    border-top:1px solid #e0e0e0;
    height:44px!important;
  }
  .v-toolbar__title .v-btn--active:before,.v-toolbar__title .v-btn:hover:before,.v-toolbar__title .v-btn:focus:before,.xs6 .v-btn--active:before,.xs6 .v-btn:hover:before,.xs6 .v-btn:focus:before{
    background:rgba(0,0,0,0);
    
  }
  .v-toolbar__title .v-btn:hover,.xs6 .v-btn:hover {
    color:#db284e;
  }
  .v-toolbar__title .v-btn--large{
    margin:6px 15px;
    min-width:0px;
    padding:0px 5px;
  }
  .v-toolbar__extension > .v-toolbar__title{
    margin-left:0px;
  }
  .banner{
    background:grey;
  }
  .banner-text{
    color:white;
    padding: 5px 400px;
  }
  .banner-text p{
    margin :1px;
  }
  .title-card-product h2{
    margin-top:12px;
    font-size: 22px;
  }
  .title-card-product p{
    margin-top:6px;
    font-size: 20px;
    color: #9b9b9b;
  }
  .title-product{
    position: absolute;
    top:-62px;
    right: -72px;
  }
  .editor-name{
    font-size: 16px;
    font-weight:500;
    color:#4a4a4a;
    margin:3px 0 0 0;
  }
  .editor-position{
    font-size: 12px;
    color:#9b9b9b;
  }
  .xs2 .v-btn--top.v-btn--absolute {
    top: -48px;
    z-index: 1;
  }
  @media (min-width: 0){
    .flex.xs2 {
          max-width: 21%;
          flex-basis: 20%;
    }
    .xs2 .v-sheet{
      border:1px solid #e0e0e0;
      border-radius: 10px;
      padding: 16px;
    }
    .xs2 .xs12 .v-responsive{
      padding:0 24px;
    }
    .xs2 .v-rating{
      margin:2px;
    }
  }
  .jumbotron-banner{
    position: absolute;
    top:24px;
    left:320px;
    width: 300px;
    color: #000;
    line-height: 1.2;
  }
  .jumbotron-title{
    font-size:26px ;
    font-weight: 700;
  }
  .jumbotron-desc{
    font-size:20px;
    font-weight: 400;
  }
  .xs4 .v-image{
    border-radius: 15px;
    margin:20px;
  }
</style>

