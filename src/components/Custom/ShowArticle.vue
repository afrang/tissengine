<template>
    <div>
        <div>
            <froalaView   dir="rtl" v-model="ctext"></froalaView>

        </div>
    </div>
</template>

<script>
    export default {
        name: "ShowArticle",
        props:['text'],
        data() {
            return {

            }

        },
        watch:{


        },
        computed:{
            ctext() {
                return  this.text.replace('%url%', this.$storage);
            }
        },
        mounted() {
            //this.show();
          this.text=this.text.replace('%url%',this.$storage);



        }
    }
</script>

<style scoped>

</style>