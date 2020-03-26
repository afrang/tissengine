<template>
    <div>
        <headers></headers>
            <show-article  :text="blog.text"></show-article>
        <div class="text-center container">
            <nav aria-label="breadcrumb" dir="rtl">
                <ol class="breadcrumb">
                    <li class="breadcrumb-item"><a href="/" class="icofont-home"></a></li>
                    <li class="breadcrumb-item"><a href="/blog" v-text="$t('blog')"></a></li>
                    <li class="breadcrumb-item " aria-current="page" v-text="blog.name"></li>
                </ol>
            </nav>
            <div class="row" dir="rtl">
                <div v-for="(item,index) in blog.article.data" :key="index" class=" col-sm-4 col-xs-12" >
                    <div class="m-1 card">
                        <a :href="'/blog/'+item.url">
                            <img v-if="item.image==1"  class="card-img-top w-100 h400 " :src="$storage+'media/Articles/'+item.id+'/thump.png'"  :title="item.name" :alt="item.name">
                            <img v-if="item.image!=1" class="card-img-top w-100 h400 "   src="/asset/icofont/nopic.png" :alt="item.name" :title="item.name">
                            <div class="card-body text-right">
                                <h5 class="mytextthumpnail card-text text-grey " v-text="item.name"></h5>
                            </div>
                        </a>
                    </div>
                </div>
            </div>
            <div class="w-100 text-center mt-5 mb-5">
                <paginate
                        :page-count="blog.article.last_page"
                        :page-range="3"
                        :margin-pages="2"
                        :click-handler="clickCallback"
                        :prev-text="$t('Prev')"
                        :next-text="$t('Next')"
                        :container-class="'pagination'"
                        :page-class="'page-item'">
                </paginate>
            </div>
        </div>
        <footers ></footers>
       </div>
</template>

<script>
    import ShowArticle from "../../components/Custom/ShowArticle";
    import headers from "../Tools/header";
    import footers from "../Tools/footer";
    import Paginate from 'vuejs-paginate'

    export default {
        name: "articlegroup",
        components:{
            headers,footers,ShowArticle,Paginate
        },
        data() {
            return {
                blog:null
            }

        },
        methods:{
            clickCallback(page){
                this.loadpage(page);

            },
            loadpage(page=1){
                let that=this;
                this.$axios.get(this.$url+'blog/'+that.$route.params.url,{
                    params: {
                        page: page
                    },
                }).then(function (res) {
                that.blog=res.data;
            });

            }
        },
    mounted() {
        this.loadpage();
    }
    }

</script>

<style scoped>
.mytextthumpnail{
    font-size: 16px !important;
    text-align: center;
    height: 50px;
    padding-top: 10px;
}
.h400{
    height: 200px;
}
    .card a{
        color:#383d41;
        text-decoration: none;
    }
.card a:hover{
    font-weight: bold;
}
</style>