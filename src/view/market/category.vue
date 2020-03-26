<template>
    <div>
        <headers></headers>
        <hr>
        <div class="container text-right" dir="rtl">
            klfkldsf
            klfkldsf
        </div>
        <footers class="mt-20"></footers>
    </div>
</template>

<script>
    import headers from "../Tools/header";
    import footers from "../Tools/footer";
    export default {
        name: "category",
        components:{
            headers,footers
        },
        data(){
          return{
              bloggroup:{}
          }
        },
        methods:{
            loadgroups:{


            }
        },
        mounted() {
            this.loadgroups();
        }
    }
</script>

<style scoped>
.mt-20{
    margin-top:300px;
}
</style>