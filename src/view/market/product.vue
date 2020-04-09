<template>
    <section>
        <headers></headers>
        <div class=" mb-4 m-10 container-fluid "  dir="rtl">
            <productdetailshow :url="url"></productdetailshow>

        </div>
        <div class="clearfix"></div>
        <footers class="mt-5"> </footers>
    </section>
</template>

<script>
    import headers from "../Tools/header";
    import footers from "../Tools/footer";
    import productdetailshow from "./productdetailshow";
    export default {
        name: "product",
        components:{
            headers,footers,productdetailshow
        },
        data(){
            return{
                url:this.$route.params.url
            }
        }
    }
</script>

<style scoped>
.m-10{
    margin-bottom: 200px !important;
}
</style>