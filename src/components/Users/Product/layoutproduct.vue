<template>
    <div class="container pt-4 text-right " dir="rtl">
        <div class="wmaster">
            <form @submit.prevent="save" dir="rtl" class="row">
                <div class="form-group col-sm-12 col-xs-12" >
                    <label  @click="loadadata()"  v-text="$t('FirstSlider')"></label>
                    <div>
                        <strong v-text="$t('slider1')"></strong>
                        <file-uploader
                                mode="layoutproduct"
                                v-on:filename="simg1"
                                :id='1'
                                name="simg1"
                                :file="mydata.simg1.data"
                        ></file-uploader>
                        <input type="text" v-model="mydata.url1.data" dir="ltr" class="form-control text-left" placeholder="url">

                    </div>
                    <div>
                        <strong v-text="$t('slider2')"></strong>
                        <file-uploader
                                mode="layoutproduct"
                                v-on:filename="simg2"
                                :id='1'
                                name="simg2"
                                :file="mydata.simg2.data"
                        ></file-uploader>
                        <input type="text" v-model="mydata.url2.data" dir="ltr" class="form-control text-left" placeholder="url">

                    </div>
                </div>
                <div class="row">
                    <div class="col-sm-3 col-xs-12">
                        <file-uploader
                                mode="layoutproduct"
                                v-on:filename="simg3"
                                :id='1'
                                name="simg3"
                                :file="mydata.simg3.data"
                        ></file-uploader>
                        <input type="text" v-model="mydata.url3.data" dir="ltr" class="form-control text-left" placeholder="url">

                    </div>
                    <div class="col-sm-3 col-xs-12">
                        <file-uploader
                                mode="layoutproduct"
                                v-on:filename="simg4"
                                :id='1'
                                name="simg4"
                                :file="mydata.simg4.data"
                        ></file-uploader>
                        <input type="text" v-model="mydata.url4.data" dir="ltr" class="form-control text-left" placeholder="url">

                    </div>
                    <div class="col-sm-3 col-xs-12">
                        <file-uploader
                                mode="layoutproduct"
                                v-on:filename="simg5"
                                :id='1'
                                name="simg5"
                                :file="mydata.simg5.data"
                        ></file-uploader>
                        <input type="text" v-model="mydata.url5.data" dir="ltr" class="form-control text-left" placeholder="url">
                    </div>
                    <div class="col-sm-3 col-xs-12">
                        <file-uploader
                                mode="layoutproduct"
                                v-on:filename="simg6"
                                :id='1'
                                name="simg6"
                                :file="mydata.simg6.data"
                        ></file-uploader>
                        <input type="text" v-model="mydata.url6.data" dir="ltr" class="form-control text-left" placeholder="url">
                    </div>
                    <div class="col-sm-12 col-xs-12">
                        <file-uploader
                                mode="layoutproduct"
                                v-on:filename="simg7"
                                :id='1'
                                name="simg7"
                                :file="mydata.simg7.data"
                        ></file-uploader>
                        <input type="text" v-model="mydata.url7.data" dir="ltr" class="form-control text-left" placeholder="url">
                    </div>
                </div>

                <input type="submit" class="btn mt-4 btn-primary" :value="$t('save')">
            </form>

        </div>

    </div>
</template>

<script>
    import FileUploader from "../../Custom/FileUploader";
    import Tisseditor from "../../Custom/Tisseditor";
    import slider1 from "../../../view/Tools/slider1";
    import VuePersianDatetimePicker from 'vue-persian-datetime-picker';
    export default {
        name: "layoutproduct",
        components: {
            FileUploader
/*            FileUploader,Tisseditor,slider1,
            datePicker: VuePersianDatetimePicker*/
        },
        data() {
            return {
                kecomponent:0,
                rawdata:{},
                modelpage:'layoutproduct',
                taglist:null,
                mydata:{

                    mode:'layoutproduct',
                    lang:'fa',
                    simg1:{
                        data:null,
                        mode:'img'
                    },
                    url1:{
                        data:null,
                        mode:'text'
                    },
                    simg2:{
                        data:null,
                        mode:'img'
                    },
                    url2:{
                        data:null,
                        mode:'text'
                    },
                    simg3:{
                        data:null,
                        mode:'img'
                    },
                    url3:{
                        data:null,
                        mode:'text'
                    },
                    simg4:{
                        data:null,
                        mode:'img'
                    },
                    url4:{
                        data:null,
                        mode:'text'
                    },
                    simg5:{
                        data:null,
                        mode:'img'
                    },
                    url5:{
                        data:null,
                        mode:'text'
                    },
                    simg6:{
                        data:null,
                        mode:'img'
                    },
                    url6:{
                        data:null,
                        mode:'text'
                    },
                    simg7:{
                        data:null,
                        mode:'img'
                    },
                    url7:{
                        data:null,
                        mode:'text'
                    },

                },
                sliders:{},
                products:{},
                artilces:{}

            }
        },
        watch:{
            rawdata:function (item) {
                let that=this;
                item.map(function (items) {
                    if(items.model=="slider"){
                        that.sliders.map(function (m) {
                            if(m.id==items.image){
                                that.mydata[items.name].data=m;
                            }

                        });
                    }
                    if(items.model=="timepicker"){
                        that.mydata[items.name].start=items.text;
                        that.mydata[items.name].end=items.image;
                    }
                    if(items.model=="tag"){
                        that.mydata[items.name].data=items.image;
                    }
                    if(items.model=="img"){
                        that.mydata[items.name].data=items.image;
                    }
                    if(items.model=="text"){
                        that.mydata[items.name].data=items.image;
                    }
                    if(items.model=="longtext"){
                        that.mydata[items.name].data=items.text;
                    }

                    if(items.model=="product"){
                        that.products.map(function (m) {

                            if(m.id==items.image){
                                that.mydata[items.name].data=m;
                            }

                        });
                    }
                    if(items.model=="article"){
                        that.artilces.map(function (m) {

                            if(m.id==items.image){
                                that.mydata[items.name].data=m;
                            }

                        });
                    }
                });
            }


        },

        methods:{
            simg1(e){
                this.mydata.simg1.data=e;
            },
            simg2(e){
                this.mydata.simg2.data=e;
            },
            simg3(e){
                this.mydata.simg3.data=e;
            },
            simg4(e){
                this.mydata.simg4.data=e;
            },
            simg5(e){
                this.mydata.simg5.data=e;
            },
            simg6(e){
                this.mydata.simg6.data=e;
            },
            simg7(e){
                this.mydata.simg7.data=e;
            },
            loadadata(){
                let that=this;
                this.$axios.get(this.$url+'user/GalleryGroup',{
                    headers:{
                        Authorization:localStorage.token
                    }
                }).then(function (response) {
                    that.sliders=response.data;
                });
                this.$axios.get(this.$url+'user/pdetail/create',{
                    headers:{
                        Authorization:localStorage.token
                    }
                }).then(function (response) {
                    that.products=response.data;
                });
                this.$axios.get(this.$url+'user/BlogArticle/create',{

                    headers:{
                        Authorization:localStorage.token
                    }
                }).then(function (response) {
                    that.artilces=response.data;
                });
                this.$axios.get(this.$url+'user/FirstPageSetting/'+this.modelpage,{
                    params:{
                        lang:that.mydata.lang
                    },
                    headers:{
                        Authorization:localStorage.token
                    }
                }).then(function (response) {
                    that.rawdata=response.data;
                });
            },
            save(){
                let that=this;
                this.$axios.post(this.$url+'user/FirstPageSetting',this.mydata,{
                    params:{
                        lang:that.mydata.lang,

                    },
                    headers:{
                        Authorization:localStorage.token
                    }
                }).then(function (response) {
                    that.$swal.fire(that.$t('saved'));
                });

            },
            loadtag(){
                let that=this;
                this.$axios.get(this.$url+'user/Tag',
                    {headers:{Authorization:localStorage.token}}
                ).then(function(res){
                    that.taglist=res.data;

                })
            }
        },
        mounted() {
            this.loadadata();
            this.loadtag();
        }
    }
</script>

<style scoped>

</style>