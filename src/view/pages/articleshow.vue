<template>
    <div>
        <headers></headers>
        <div  dir="rtl" class="m-2">
            <div class="container-fluid">
                <nav aria-label="breadcrumb" dir="rtl">
                    <ol class="breadcrumb">
                        <li class="breadcrumb-item"><a href="/" class="icofont-home"></a></li>
                        <li class="breadcrumb-item"><a href="/blog" v-text="$t('blog')"></a></li>
                        <li class="breadcrumb-item"><a :href="'/group/'+blog.to_article.url" v-text="$t(blog.to_article.name)"></a></li>
                        <li  class="breadcrumb-item " aria-current="page" v-text="blog.name"></li>
                    </ol>
                </nav>
            </div>
            <h1 v-text="blog.name" class="text-right"></h1>
            <hr>
            <show-article  dir="rtl" :text="blog.text"></show-article>
            <hr>
            <div dir="rtl" class="text-right container">
                <a v-for="(item,index) in blog.totags" :href="'/tag/'+item.name" :key="index"  dir="rtl" class="badge badge-dark icofont-1x">#<span v-text="item.name"></span></a>
            </div>

        </div>
        <footers class="myfootertop"></footers>
    </div>
</template>

<script>
    import ShowArticle from "../../components/Custom/ShowArticle";
    import headers from "../Tools/header";
    import footers from "../Tools/footer";
    export default {
        name: "articleshow",
        components:{
            headers,footers,ShowArticle
        },
        data() {
            return {
                blog:null
            }

        },
        methods:{

            loadpage(){
                let that=this;
                this.$axios.get(this.$url+'article',{
                    params:{
                        url:that.$route.params.url
                    }
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
    .myfootertop{
        margin-top: 200px;
    }
</style>