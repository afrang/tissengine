<template>
    <div class="row">
        <modal v-if="masterimg!=null" name="demo-login" transition="pop-out" :width="modalWidth"  :height="500"   dir="ltr">
            <div class="box">
                <div class="box-part" id="bp-left">
                    <div class="partition" id="partition-register">
                        <div class="partition-title" dir="rtl" v-text="product.name"></div>
                        <div class="partition-form" style="overflow-y: auto; height: 100%; ">
                            <ul class="myitemimages">
                                <template  v-for="(item,index) in product.to_image">
                                    <li :key="index"  class="tiss-cursur" @click="changepicture(item)">
                                        <img  :src="$storage+'media/Product/'+product.id+'/thump/'+item.file" width="100%">
                                    </li>
                                </template>
                            </ul>
                        </div>
                    </div>
                </div>
                <div class="box-part" id="bp-right" >
                        <img  style="width: 100%;" :src="$storage+'media/Product/'+product.id+'/medium/'+masterimg.file"  >
                </div>
            </div>
        </modal>

        <div class="col-sm-5 col-xs-12" >
            <template v-if="masterimg!=null">
                <div >
                    <img class="w-100 " :src="$storage+'media/Product/'+product.id+'/medium/'+masterimg.file">
                </div>
                <ul class="myitemimage">
                    <template  v-for="(item,index) in product.to_image">
                        <li :key="index" v-if="index<=4"  class="tiss-cursur" @click="changepicture(item)">
                            <img  :src="$storage+'media/Product/'+product.id+'/thump/'+item.file">
                            <div class="moreimage" v-if="index==4" @click="show">
                                <i class="icofont-multimedia icofont-2x text-white"></i>
                            </div>

                        </li>
                    </template>

                </ul>
            </template>

        </div>
        <div class="col-sm-4 col-xs-12 mydetailnumber">
            <h1 v-text="product.name"></h1>
            <h4 v-text="product.model"></h4>
            <div class="row text-right" dir="rtl ">
                <div class="col-sm-6">
                    <span v-text="$t('category')"></span><a :href="'/category/'+product.to_group.url" v-text="product.to_group.name"></a>
                </div>
            </div>
            <div class="row text-right" dir="rtl ">
                <div class="col-sm-6">
                <span v-text="$t('color')"></span>:
                </div>
            </div>
            <span @click="loadproduct">pciture</span>

            <pre>{{ product.to_color }}</pre>
        </div>
        <div class="col-sm-3 col-xs-12">

        </div>
    </div>
</template>

<script>
    const MODAL_WIDTH = 1024

    export default {
        name: "productdetailshow",
        props:['url'],
        data(){
            return{
                product:null,
                masterimg:null,
                modalWidth: MODAL_WIDTH

            }
        },
        computed:{

        },
        methods:{
            show () {
                this.$modal.show('demo-login');
            },
            hide () {
                this.$modal.hide('demo-login');
            },
            changepicture(item){
                this.masterimg=item;
            },
            mainpage(){
                let that=this;
                this.product.to_image.filter(function (item) {
                    if(item.master==1){
                        that.masterimg=item;
                    }
                })
            },
            loadproduct(){
                let that=this;

                this.$axios.get(this.$url+'product/'+this.url)
                    .then(function (res) {
                        that.product=res.data;
                        that.mainpage();
                    })
            }
        },
        mounted() {
            this.loadproduct();
            this.show();
        }
        ,created () {
            this.modalWidth = window.innerWidth < MODAL_WIDTH
                ? MODAL_WIDTH / 2
                : MODAL_WIDTH
        }

    }
</script>

<style lang="scss">

    $background_color: #404142;
    $github_color: #DBA226;
    $facebook_color: #3880FF;
    .mydetailnumber h1{
        direction: rtl;
        text-align: right;
        font-size: 25px;
        color: #9d9d9d;
    }
    .mydetailnumber h4{
        text-align: right;
        color: rgba(141, 141, 141, 0.56);
        font-size: 14px;
        font-weight: bold;
        border-bottom: solid 1px rgba(141, 141, 141, 0.38);
    }
    .box {
        background: white;
        overflow: hidden;
        height: 100%;
        border-radius: 2px;
        box-sizing: border-box;
        box-shadow: 0 0 40px black;
        color: #8b8c8d;
        font-size: 0;
        .box-part {
            display: inline-block;
            position: relative;
            vertical-align: top;
            box-sizing: border-box;
            height: 100%;
            width: 30%;
            &#bp-right {
                width: 70%;
                border-left: 1px solid #eee;
            }
        }
        .box-messages {
            position: absolute;
            left: 0;
            bottom: 0;
            width: 100%;
        }
        .box-error-message {
            position: relative;
            overflow: hidden;
            box-sizing: border-box;
            height: 0;
            line-height: 32px;
            padding: 0 12px;
            text-align: center;
            width: 100%;
            font-size: 11px;
            color: white;
            background: #F38181;
        }
        .partition {
            width: 100%;
            height: 100%;
            .partition-title {
                box-sizing: border-box;
                padding: 30px;
                width: 100%;
                text-align: center;
                letter-spacing: 1px;
                font-size: 20px;
                font-weight: 300;
            }
            .partition-form {
                padding: 0 20px;
                box-sizing: border-box;
            }
        }
        input[type=password],
        input[type=text] {
            display: block;
            box-sizing: border-box;
            margin-bottom: 4px;
            width: 100%;
            font-size: 12px;
            line-height: 2;
            border: 0;
            border-bottom: 1px solid #DDDEDF;
            padding: 4px 8px;
            font-family: inherit;
            transition: 0.5s all;
            outline: none;
        }
        button {
            background: white;
            border-radius: 4px;
            box-sizing: border-box;
            padding: 10px;
            letter-spacing: 1px;
            font-family: "Open Sans", sans-serif;
            font-weight: 400;
            min-width: 140px;
            margin-top: 8px;
            color: #8b8c8d;
            cursor: pointer;
            border: 1px solid #DDDEDF;
            text-transform: uppercase;
            transition: 0.1s all;
            font-size: 10px;
            outline: none;
            &:hover {
                border-color: mix(#DDDEDF, black, 90%);
                color: mix(#8b8c8d, black, 80%);
            }
        }
        .large-btn {
            width: 100%;
            background: white;
            span {
                font-weight: 600;
            }
            &:hover {
                color: white !important;
            }
        }
        .button-set {
            margin-bottom: 8px;
        }
        #register-btn,
        #signin-btn {
            margin-left: 8px;
        }
        .facebook-btn {
            border-color: $facebook_color;
            color: $facebook_color;
            &:hover {
                border-color: $facebook_color;
                background: $facebook_color;
            }
        }
        .github-btn {
            border-color: $github_color;
            color: $github_color;
            &:hover {
                border-color: $github_color;
                background: $github_color;
            }
        }
        .autocomplete-fix {
            position: absolute;
            visibility: hidden;
            overflow: hidden;
            opacity: 0;
            width: 0;
            height: 0;
            left: 0;
            top: 0;
        }
    }
    .pop-out-enter-active,
    .pop-out-leave-active {
        transition: all 0.5s;
    }
    .pop-out-enter,
    .pop-out-leave-active {
        opacity: 0;
        transform: translateY(24px);
    }
    .myitemimage{
        width: 100%;
        white-space: nowrap; /* This is required unless you put the helper span closely near the img */
        margin: 1em 0;
        height: 50px;

    }
.myitemimage li{
    float: right;
    list-style: none;
    border-collapse: separate;
    border-spacing: 15px;
    border: solid 1px #a3a3a3;
    margin: 1px;
    width: 18%;
    vertical-align: center;
    horiz-align: center;
    border-radius: 5px;
    display: flex;
    height: 100%;
    position: relative;
    justify-content: center;
    align-items: center;
    padding: 10px;


}
    .myitemimage li:hover{
        border: solid 1px #848484;
    }
    .myitemimage li   img{width: 100%;
        vertical-align: middle;
        max-height: 50px;

    }
    .moreimage{
        position: absolute;


    }
    .myitemimages{
        width: 100%;
        white-space: nowrap; /* This is required unless you put the helper span closely near the img */
        margin: 1em 0;
        height: 70px;

    }
.myitemimages li{
    float: right;
    list-style: none;
    border-collapse: separate;
    border-spacing: 15px;
    border: solid 1px #a3a3a3;
    margin: 1px;
    width: 32%;
    vertical-align: center;
    horiz-align: center;
    border-radius: 5px;
    display: flex;
    height: 100%;
    position: relative;
    justify-content: center;
    align-items: center;
    padding: 10px;

}
    .myitemimage li   img{width: 100%;
        vertical-align: middle;
        max-height: 70px;

    }
</style>