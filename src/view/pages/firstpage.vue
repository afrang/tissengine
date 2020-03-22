<template>
    <div>
        <headers></headers>
        <slider1 class="myslider" height="320" :id="firsptagedata[0].image" :name="'topslider'"></slider1>

        <div class="bg-yellow">
            <div class="container" dir="">
                <div class="row">


                    <div class="col-sm-4 col-xs-12 p-4" dir="rtl" >
                        <div class="row">
                            <div class="col-sm-12 text-center">
                                <a :href="firsptagedata[11].text">
                                    <countdown
                                            v-if="firsptagedata[24].text!=null"
                                            style="position: absolute; margin-top:6px; margin-left: -20px;"
                                            trans='{
                                         "day":"Day",
                                         "hours":"Hours",
                                         "minutes":"Minuts",
                                         "seconds":"Seconds",
                                         "expired":"Event has been expired.",
                                         "running":"Till the end of event.",
                                         "upcoming":"Till start of event.",
                                         "status": {
                                            "expired":"Expired",
                                            "running":"Running",
                                            "upcoming":"Future"
                                           }}'
                                            :starttime='[ firsptagedata[24].text, "jYYYY/jMM/jDD HH:mm" ] | moment("MMM D, YYYY hh:mm:00")'
                                            :endtime='[ firsptagedata[24].image, "jYYYY/jMM/jDD HH:mm" ] | moment("MMM D, YYYY hh:mm:00")' ></countdown>

                                    <img  class="img-thumbnail w-100" style="height: 190px;"  :src="$storage+'media/firspage/1/thump/'+firsptagedata[3]['image']" >
                                </a>

                            </div>
                            <div class="col-sm-12 mt-4" >
                                <countdown
                                        v-if="firsptagedata[25].text!=null"
                                        style="position: absolute; margin-top:6px; margin-left: -20px;"
                                        trans='{
                                         "day":"Day",
                                         "hours":"Hours",
                                         "minutes":"Minuts",
                                         "seconds":"Seconds",
                                         "expired":"Event has been expired.",
                                         "running":"Till the end of event.",
                                         "upcoming":"Till start of event.",
                                         "status": {
                                            "expired":"Expired",
                                            "running":"Running",
                                            "upcoming":"Future"
                                           }}'
                                        :starttime='[ firsptagedata[25].text, "jYYYY/jMM/jDD HH:mm" ] | moment("MMM D, YYYY hh:mm:00")'
                                        :endtime='[ firsptagedata[25].image, "jYYYY/jMM/jDD HH:mm" ] | moment("MMM D, YYYY hh:mm:00")' ></countdown>
                                <img class="img-thumbnail w-100" style="height: 190px;"   :src="$storage+'media/firspage/1/thump/'+firsptagedata[2]['image']" >
                            </div>
                        </div>
                    </div>
                    <div class="col-sm-8 col-xs-12 p-4" >
                        <slider2  :id="firsptagedata[1].image"></slider2>
                    </div>
                </div>
            </div>
        </div>
        <template v-if="listspecial!=null">
            <carousel :perPage="5">
                <slide  v-for="(item,index) in listspecial.data" :key="index" class="m-1"  >
                    <a class="removedecration" :href="'/product/'+item.url">
                    <div class="card "  style="border-radius: 45px;" >
                        <img  v-if="item.image!=null" class="card-img-top h400" :src="$storage+'media/Product/'+item.id+'/thump/'+item.image" :alt="item.name">
                        <img  v-if="item.image==null"  class="card-img-top h400" src="/asset/icofont/nopic.png" :alt="item.name">
                            <div class="card-text text-center tiss-thumpbox">
                                <div class="row">
                                    <div class="col-sm-12 text-right">
                                        <span v-if="item.percent!=null" class="badge badge-danger float-left" v-text="item.percent+ '%'"></span>
                                        <p v-text="item.group" class="yellowtext"></p>
                                        <h5 class="m--4" dir="rtl"><span v-text="item.name" class="font-weight-bolder"></span> <small class="text-blue font-weight-bolder m--4" v-text="item.model"></small></h5>
                                    </div>
                                    <div class="col-sm-6 text-right myitems  redlies " >
                                        <template v-if="item.price!=null">
                                            <small v-text="$t('toman')"></small>
                                            <vue-numeric dir="rtl" :read-only="true"  separator="," v-model="item.price"></vue-numeric>
                                        </template>
                                    </div>
                                    <div class="col-sm-6 myitems text-right greentext">
                                        <template v-if="item.discount!=null">
                                        <small v-text="$t('toman')"></small>
                                        <vue-numeric dir="rtl" :read-only="true"   class="mainprice"  separator="," v-model="item.discount"></vue-numeric>
                                        </template>
                                    </div>
                                </div>
                        </div>
                    </div>
                    </a>
                </slide>

            </carousel>
        </template>

        <div class="container">
            <div class=" row mt-3 productfirst">
                <div class="col-sm-6 col-xs-12 text-center">
                    <a href="/prodcut/">
                        <div class="img-hover-zoom">
                            <img :src="$storage+'media/firstpage/1/orginal/'+firsptagedata[8].image" class="w-100" style="border-radius: 5px;">

                        </div>
                        <div class="container">
                            <div v-if="product.prs!=null" class="row mt-2 mypricespecial" >
                                <div class="col-sm-6 text-left">
                                    <div class="col-sm-6 myitems text-right greentext">
                                        <template v-if="product.prs.data.price!=null">
                                            <small v-text="$t('toman')"></small>
                                            <vue-numeric dir="rtl" :read-only="true"  separator="," v-model="item.price"></vue-numeric>
                                        </template>
                                        <template v-if="product.prs.data.discount!=null">
                                            <small v-text="$t('toman')"></small>
                                            <vue-numeric dir="rtl" :read-only="true"   class="mainprice"  separator="," v-model="product.prs.data.discount"></vue-numeric>
                                        </template>
                                    </div>

                                    <star-rating style="margin-top: -10px;" star-size="20" :glow="20" :round-start-rating="false"  :read-only="true" :show-rating="false" :rating="2.5" class="w-100"></star-rating>

                                </div>
                                <div class="col-sm-6 text-right" dir="rtl">
                                    <h5>{{ product.prs.data.name }} <small>{{ product.prs.data.model }}</small></h5>
                                    <p>{{ product.prs.data.group }}</p>
                                </div>

                            </div>
                        </div>
                    </a>

                </div>
                <div class="col-sm-6 col-xs-12">
                    <div class="row">
                        <div class="col-sm-6"  v-for="(n, index) in 4"  :key="index">
                            <template v-if="product['pr'+(index+1)]!=null" >
                            <div class="img-hover-zoom">

                                <img  v-if="product['pr'+(index+1)].data.image!=null" height="320px;" class="w-100" style="border-radius: 5px;" :src="$storage+'media/Product/'+product['pr'+(index+1)].data.id+'/thump/'+product['pr'+(index+1)].data.image" :alt="product['pr'+(index+1)].data.name">
                                <img  v-if="product['pr'+(index+1)].data.image==null"  height="320px;" class="w-100" style="border-radius: 5px;" src="/asset/icofont/nopic.png" :alt="product['pr'+(index+1)].data.name">

                            </div>
                            <div class="row mt-2 mypricespecial" >
                                <div class="col-sm-4">
                                    <star-rating style="margin-top: -10px;" star-size="20" :glow="20" :round-start-rating="false"  :read-only="true" :show-rating="false" :rating="2.5" class="w-100"></star-rating>

                                    <template v-if="product['pr'+(index+1)].data.price!=null">
                                        <small v-text="$t('toman')"></small>
                                        <vue-numeric dir="rtl" :read-only="true"  separator="," v-model="product['pr'+(index+1)].data.price"></vue-numeric>
                                    </template>

                                </div>
                                <div class="col-sm-8 text-right" dir="rtl">
                                    <h5 >{{ product['pr'+(index+1)].data.name }} <small>{{ product['pr'+(index+1)].data.model }}</small></h5>
                                    <p>{{ product['pr'+(index+1)].data.group }}</p>
                                </div>

                            </div>
                            </template>
                        </div>

                    </div>

                </div>
            </div>
        </div>
        <div @click="options">dsd</div>
        <pre>{{ product }}</pre>


    </div>
</template>

<script>
    import headers from "../Tools/header";
    import slider1 from "../Tools/slider1";
    import slider2 from "../Tools/slider2";
    import countdown from "../Tools/countdown";
    import StarRating from 'vue-star-rating';
    import { Carousel, Slide } from 'vue-carousel';
    import VueNumeric from 'vue-numeric';



    export default {
        name: "firstpage",
        components:{
            slider1,
            slider2,
            headers,
            countdown,
            StarRating,
            Carousel,
            Slide,
            VueNumeric,

        },
        watch :{

        },

        data: () => ({
                firsptagedata:{},
            listspecial:null,
            moneyslide:{
                decimal: ',',
                thousands: ',',
                prefix:'تومان',
                suffix: ' ',
                precision: 0,
                masked: false
            },
            product:{
                prs:null,
                pr1:null,
                pr2:null,
                pr2:null,
                pr3:null

            }
        }),

        methods:{
            loaddata(){
                let that=this;
                this.$axios.get(this.$url+'firstpage').then(function (res) {
                    that.firsptagedata=res.data;
                    that.options();
                });
            },
            options(){
                let that=this;
                this.$axios.get(this.$url+'searchproduct',{
                    params: {
                        tag:that.firsptagedata[26].image

                    },
                    headers:{Authorization:localStorage.token}
                }).then(function (res) {
                    that.listspecial=res.data;
                });

                this.$axios.get(this.$url+'searchproduct/'+this.firsptagedata[17].image,{
                    params: {

                    },
                    headers:{Authorization:localStorage.token}
                }).then(function (res) {
                    that.product.prs=res.data;
                });

                this.$axios.get(this.$url+'searchproduct/'+this.firsptagedata[15].image,{
                    params: {

                    },
                    headers:{Authorization:localStorage.token}
                }).then(function (res) {
                    that.product.pr1=res.data;
                });
                this.$axios.get(this.$url+'searchproduct/'+this.firsptagedata[16].image,{
                    params: {

                    },
                    headers:{Authorization:localStorage.token}
                }).then(function (res) {
                    that.product.pr2=res.data;
                });
                this.$axios.get(this.$url+'searchproduct/'+this.firsptagedata[17].image,{
                    params: {

                    },
                    headers:{Authorization:localStorage.token}
                }).then(function (res) {
                    that.product.pr3=res.data;
                });
                this.$axios.get(this.$url+'searchproduct/'+this.firsptagedata[18].image,{
                    params: {

                    },
                    headers:{Authorization:localStorage.token}
                }).then(function (res) {
                    that.product.pr4=res.data;
                });
            }
        },
        mounted() {
            this.loaddata();
        }
    }
</script>

<style scoped>
    .redlies{
        text-decoration:line-through;
    }
.mypricespecial{
    text-decoration: none;
    color:#333333;;

}
.mainprice{
    font-size: 18px; color: red;
}
.mypricespecial  * h5{
    font-size:14px;
    font-weight: bolder;
    color:dimgray;;

}
    .mypricespecial  * p{
        font-size:10px;
        font-weight: bolder;
        color:dimgray;;

    }
.myitems{
    margin-top: -5px;
    font-weight: bolder;
}
.bg-yellow{
    background-color:yellow ;
}
    .mytitleproduct div h5{
        color: #666666;;
        font-weight: bolder;
        font-size: 24px;
        margin-right: 10px;
    }
    .mytitleproduct p{
        padding-right: 20px;
        direction: rtl;
    }
    .productfirst div a{
        text-decoration: none;


    }
.productfirst div p {
    color: #666;
    font-weight: bold;

}
/* [1] The container */
.img-hover-zoom {
    overflow: hidden; /* [1.2] Hide the overflowing of child elements */
}

/* [2] Transition property for smooth transformation of images */
.img-hover-zoom img {
    transition: transform 1s ease;
}

/* [3] Finally, transforming the image when container gets hovered */
.img-hover-zoom:hover img {
    transform: scale(1.2);
}
    .tiss-thumpbox{
        margin: 10px;
        border-radius: 4px;
        margin-top: -125px;
        background-color: #ffffff;
        padding: 10px;
        height: 78px;
        line-height: 1;


    }
    .h400{
        height: 400px;
        overflow: hidden;
    }
    .yellowtext{
        color: #e0ab0f;
    }.m--4{
             margin-top: -11px;
         }
    .greentext{
        color: #e0670b;
    }
    .removedecration{
        text-decoration: none;
        color: gray;
    }
</style>