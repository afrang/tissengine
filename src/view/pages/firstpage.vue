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
        <carousel>
            <slide>
                Slide 1 Content
            </slide>
            <slide>
                Slide 2 Content
            </slide>
        </carousel>
        <div class="container">
            <div class=" row mt-3 productfirst">
                <div class="col-sm-6 col-xs-12 text-center">
                    <a href="/prodcut/">
                        <div class="img-hover-zoom">
                            <img :src="$storage+'media/firstpage/1/orginal/'+firsptagedata[8].image" class="w-100" style="border-radius: 5px;">

                        </div>
                        <div class="container">
                            <div class="row mt-2 mypricespecial" >
                                <div class="col-sm-6 text-left">
                                    <p> 500000 <span v-text="$t('toman')"></span> </p>
                                    <star-rating style="margin-top: -10px;" star-size="20" :glow="20" :round-start-rating="false"  :read-only="true" :show-rating="false" :rating="2.5" class="w-100"></star-rating>

                                </div>
                                <div class="col-sm-6 text-right" dir="rtl">
                                    <h5>نمونه <small>5xe4</small></h5>
                                    <p>گروه فلان </p>
                                </div>

                            </div>
                        </div>
                    </a>

                </div>
                <div class="col-sm-6 col-xs-12">
                    <div class="row">
                        <div class="col-sm-6" v-for="(n, index) in 4"  :key="index">
                            <div class="img-hover-zoom">
                                <img :src="$storage+'media/firstpage/1/orginal/'+firsptagedata[8].image" height="320px;" class="w-100" style="border-radius: 5px;">

                            </div>
                            <div class="row mt-2 mypricespecial" >
                                <div class="col-sm-6">
                                    <p> 500000 <span v-text="$t('toman')"></span> </p>
                                    <star-rating style="margin-top: -10px;" star-size="20" :glow="20" :round-start-rating="false"  :read-only="true" :show-rating="false" :rating="2.5" class="w-100"></star-rating>

                                </div>
                                <div class="col-sm-6 text-right" dir="rtl">
                                    <h5>نمونه <small>5xe4</small></h5>
                                    <p>گروه فلان </p>
                                </div>

                            </div>

                        </div>

                    </div>

                </div>
            </div>
        </div>

        <pre>{{ firsptagedata[26] }}</pre>
    </div>
</template>

<script>
    import headers from "../Tools/header";
    import slider1 from "../Tools/slider1";
    import slider2 from "../Tools/slider2";
    import countdown from "../Tools/countdown";
    import StarRating from 'vue-star-rating';
    import { Carousel, Slide } from 'vue-carousel';



    export default {
        name: "firstpage",
        components:{
            slider1,
            slider2,
            headers,
            countdown,
            StarRating,
            Carousel,
            Slide
        },
        watch :{

        },

        data: () => ({
                firsptagedata:{}
        }),

        methods:{
            loaddata(){
                let that=this;
                this.$axios.get(this.$url+'firstpage').then(function (res) {
                    that.firsptagedata=res.data;
                })
            }
        },
        mounted() {
            this.loaddata();
        }
    }
</script>

<style scoped>
.mypricespecial{
    text-decoration: none;
    color:#333333;;

}
.mypricespecial  * h5{
    font-size: 24px;
    font-weight: bolder;
    color:dimgray;;

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
</style>