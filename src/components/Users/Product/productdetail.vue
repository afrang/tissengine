<template>
    <div class="container pt-4">
        <!-- Modal -->

       <div class="wmaster text-right" dir="rtl">
           <modal   scrollable="true"   height="auto" name="hello-world" dir="ltr" :key="'mi'"  >
               <div class="modal-content">
                   <div class="modal-header text-right" >
                       <h5 class="modal-title text-right w-100" dir="rtl" v-text="$t('coloroption')"></h5>
                   </div>
                   <div class="modal-body">
                   <form  @submit.prevent="savecolor"  dir="rtl" v-if="coloredit!=null" class="form text-right row" >

                       <div class="form-group col-sm-12">
                       <a   class="btn   text-white m-1 w-100 text-right" >
                           <div  class="btncolor" :style="{ 'background-color': coloredit['to_color']['code'] }"></div>
                           <a v-text="coloredit['to_color']['name']" style="color: #333;" class="text-black"></a>

                       </a>
                       </div>

                        <div class="form-group container col-sm-6 ">

                            <label v-text="$t('existing')"></label>
                            <select v-model="coloredit.existing" class="form-control">
                                <option value="1" v-text="$t('yes')"></option>
                                <option value="0" v-text="$t('no')"></option>
                            </select>
                            <hr>
                            <button  type="submit" class="btn btn-primary" v-text="$t('save')"></button>
                        </div>
                       <div class="form-group col-sm-6">
                           <file-uploader
                                   :key="'fa'+1"
                                   mode="Product"
                                   v-on:filename="iamgemanagers"
                                   :id='product.id'
                                   :showthump="true"
                                   :name=coloredit.color
                                   :deletefile="true"
                                   :file="coloredit.image"
                           ></file-uploader>

                       </div>




                   </form>
                   </div>
                   </div>
           </modal>

           <h4 v-text="$t('product')"></h4>
           <hr>
           <a @click="add" class="btn btn-success icofont-ui-add p-3 text-white"></a>
           <a @click="listproduct()" class="btn btn-success icofont-listing-box  mr-4 p-3 text-white"></a>
           <hr>
           <p @click="listgroup"  v-text="mode"></p>

           <template v-if="mode=='list'">

               <table class="table  table-striped">

                   <thead>
                   <tr>
                       <th scope="col">#</th>
                       <th scope="col" v-text="$t('name')"></th>
                       <th scope="col" v-text="$t('model')"></th>
                       <th scope="col" v-text="$t('group')"></th>
                       <th  class="text-center" scope="col" v-text="$t('action')"></th>
                   </tr>
                   </thead>
                   <tbody>
                   <tr v-for="(item,index) in listitems.data"  :key="'far'+index">
                       <th scope="row" v-text="index+1"></th>
                       <td v-text="item.name"></td>
                       <td v-text="item.model"></td>
                       <td v-text="item.group"></td>
                       <td class="text-center" >
                           <button  @click="edit(item.id)" class="btn btn-success icofont-ui-edit"></button>
                           <button  @click="del(item.id)" class="btn btn-danger mr-2 icofont-ui-delete"></button>
                       </td>
                   </tr>

                   </tbody>
               </table>
           </template>
           <template v-if="mode=='edit'">

               <form @submit.prevent="save" class="row">

                   <div class="form-group col-sm-6 col-xs-12">
                       <label  v-text="$t('name')"></label>
                       <input @keyup="urlcreate" type="text" v-model="product.name" class="form-control" :placeholder="$t('name')">
                       <small  class="form-text text-muted"></small>
                   </div>
                   <div class="form-group col-sm-6 col-xs-12">
                       <label v-text="$t('url')"></label>
                       <input   type="text" v-model="product.url" class="form-control"  :placeholder="$t('url')">
                       <small  class="form-text text-muted"></small>
                   </div>
                   <div class="form-group col-sm-6 col-xs-12" v-if="product.id==null">
                       <label v-text="$t('group')"></label>
                       <select v-model="product.parent" class="form-control">
                           <template v-for="(item,index) in group" >
                               <option  v-if="item.to_sub.length==0" :key="'fars'+index" :value="item.id" v-text="item.name"></option>
                               <optgroup   v-if="item.to_sub.length!=0"  :key="'farsi'+index"  :label="item.name">
                                   <option v-for="(items,index2) in item.to_sub" :key="'farsia'+index2"  :value="items.id" v-text="items.name"></option>
                               </optgroup>

                           </template>

                       </select>
                       <small  class="form-text text-muted"></small>
                   </div>
                   <div class="container" v-if="product.id!=null">
                       <br>
                       <!-- Nav tabs -->
                       <ul class="nav nav-tabs" role="tablist">
                           <li class="nav-item">
                               <a class="nav-link active" data-toggle="tab" href="#home" v-text="$t('specifications')" ></a>
                           </li>
                           <li class="nav-item">
                               <a class="nav-link" data-toggle="tab" href="#menu1"  v-text="$t('images')" ></a>
                           </li>
                           <li class="nav-item">
                               <a class="nav-link" data-toggle="tab" href="#menu2"   v-text="$t('PricingFeature')"></a>
                           </li>

                           <li class="nav-item">
                               <a class="nav-link" data-toggle="tab" href="#menu3"   v-text="$t('Attribute')"></a>
                           </li>
                           <li class="nav-item">
                               <a class="nav-link" @click="loadcolor" data-toggle="tab" href="#menu4"   v-text="$t('colormanager')"></a>
                           </li>
                           <li class="nav-item">
                               <a class="nav-link" data-toggle="tab" href="#review"   v-text="$t('description')"></a>
                           </li>
                       </ul>

                       <!-- Tab panes -->
                       <div class="tab-content ">
                           <div id="home" class="container tab-pane active pb-5"><br>
                               <h3  v-text="$t('specifications')"></h3>
                               <div class="row">
                               <div class="form-group col-sm-6 col-xs-12">
                                   <label v-text="$t('title')"></label>
                                   <input   type="text" v-model="product.title" class="form-control"  :placeholder="$t('title')">
                                   <small  class="form-text text-muted"></small>
                               </div>
                               <div class="form-group col-sm-6 col-xs-12">
                                   <label v-text="$t('model')"></label>
                                   <input   type="text" v-model="product.model" class="form-control"  :placeholder="$t('model')">
                                   <small  class="form-text text-muted"></small>
                               </div>

                                   <div class="form-group col-sm-6 col-xs-12">
                                       <label v-text="$t('status')"></label>
                                       <select class="form-control" v-model="product.status">
                                           <option v-for="(item,index) in status" :key="'farsian'+index" :value="index" v-text="item"></option>
                                       </select>
                                       <small  class="form-text text-muted"></small>
                                   </div>


                                   <div class="form-group col-sm-6 col-xs-12">
                                       <label v-text="$t('special')"></label>
                                       <select class="form-control" v-model="product.special">
                                           <option v-for="(item,index) in special" :key="'p'+index" :value="index" v-text="item"></option>
                                       </select>
                                       <small  class="form-text text-muted"></small>
                                   </div>
                                   <div class="form-group col-sm-6 col-xs-12">
                                       <label v-text="$t('discount')"></label>
                                       <select class="form-control" v-model="product.special">
                                           <option v-for="(item,index) in booleanarray" :key="'pe'+index" :value="index" v-text="item"></option>
                                       </select>
                                       <small  class="form-text text-muted"></small>
                                   </div>
                                   <div class="form-group col-sm-6 col-xs-12">
                                       <label v-text="$t('expressdelivery')"></label>
                                       <select class="form-control" v-model="product.expressdelivery">
                                           <option v-for="(item,index) in booleanarray" :key="'per'+index" :value="index" v-text="item"></option>
                                       </select>
                                       <small  class="form-text text-muted"></small>
                                   </div>

                                   <div class="form-group col-sm-12 col-xs-12">
                                       <vue-tags-input class="col-xs-12"
                                                       :key="'pers'+1"
                                                       v-model="tag"
                                                       :tags="tags"
                                                       @tags-changed="newTags => tags = newTags"
                                                       :autocomplete-items="filteredItems"
                                       />
                                       <h3 v-text="$t('abstract')"></h3>
                                   <p>
                                       <tisseditor  :key="'pers'+1"  :text="product.morecomment" v-on:myevent="morecommentedit"   :mode="'Product'"></tisseditor>
                                   </p>
                                   </div>
                               </div>
                               </div>
                           <div id="menu1" class="container tab-pane fade"><br>
                               <h3  @click="loadimage" v-text="$t('images')"></h3>
                               <div class="row">
                                   <div class="col-sm-3">
                                       <file-uploader
                                               :key="'persi'+1"
                                               mode="Product"
                                               v-on:filename="addpicture"
                                               :id='product.id'
                                               :showthump="false"
                                               name="random"
                                               :deletefile="false"
                                               :file="group.thump"
                                       ></file-uploader>
                                   </div>
                                   <div class="col-sm-8 pb-5 ">
                                        <div class="row">
                                            <div  v-for="(item,index) in imagelist" :key="'persia'+index" class="col-sm-4  mt-2 col-xs-12">
                                                <div class="card"  >
                                                    <img class="card-img-top" :src="$storage+'media/Product/'+product.id+'/thump/'+item.file" alt="Card image cap">
                                                    <div class="card-body">
                                                        <a @click="delimage(item.id)" class="btn btn-primary icofont-2x icofont-ui-delete" ></a> |
                                                        <a v-if="item.master==0" @click="masterimg(item.id)" :title="$t('masteriamge')" class=" btn btn-danger  icofont-2x icofont-toggle-off"></a>
                                                        <a   v-if="item.master==1"   :title="$t('masteriamge')" class=" btn btn-primary  icofont-2x icofont-toggle-on"></a>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                   </div>
                               </div>
                               <p>

                               </p>
                           </div>
                           <div id="menu4" class="container tab-pane fade"><br>
                               <h3 v-text="$t('colormanager')"></h3>
                               <hr>
                               <label v-text="$t('modecolor')"></label>
                               <select v-model="product.colormode" class="form-control">
                                   <option value="1" v-text="$t('includedcolor')"></option>
                                   <option value="2" v-text="$t('colortypecolor')"></option>
                               </select>
                               <h4  v-text="$t('listcolor')"></h4>
                               <ul class="row mylistcolor">
                               <li class="col-sm-2  "  @click="addtocolorexist(item.id)"  v-for="(item,index) in product.to_group.to_color" :key="'persian'+index"  >
                                   <div  class="btn text-white m-1 w-100 text-right" >
                                           <div  class="btncolor" :style="{ 'background-color': item.code }"></div>
                                       <a class="icofont-ui-add"></a> |

                                       <a v-text="item.name"></a>
                                   </div>
                               </li>
                               </ul>

                               <hr>
                               <h4 v-text="$t('listexist')"></h4>
                               <hr>
                               <ul class="row mylistcolor">
                               <li class="col-sm-4  w-100 text-right "  v-for="(item,index) in listcolor" :key="'es'+index"  >
                                   <span @click="colororderup(item.id)" class="icofont-arrow-right float-right btn text-white m-1"></span>
                                   <a   class="btn   text-white " >
                                       <div  class="btncolor" :style="{ 'background-color': item.to_color.code }"></div>
                                       <a  @click="editcolor(index)"  class="icofont-ui-edit"></a> |
                                       <span @click="deletecolor(item.id)" class="icofont-ui-delete "></span>

                                      | <a v-text="item.to_color.name"></a>
                                   </a>
                                   <span @click="colororderdown(item.id)" class="icofont-arrow-left float-left btn text-white  m-1 "></span>


                               </li>
                               </ul>
                           </div>

                           <div id="menu2" class="container tab-pane fade"><br>

                               <h3 v-text="$t('fatureandprice')"></h3>
                               <label v-text="$t('price')"></label>
                               <money dir="ltr"  class="form-control" v-model="price" v-bind="money"></money>
                               <label v-text="$t('pricediscount')"></label>
                               <money dir="ltr"  class="form-control" v-model="discount" v-bind="money"></money>
                               <label v-text="$t('percent')"></label>
                               %  <input class="form-control w-25" type="number" min="0" max="100" v-model="percent">

                               <input type="button" class="btn btn-primary mt-4" @click="newpricesubmit" :value="$t('save')">
                               <hr>
                               <div class="container">
                                   <h4 v-text="$t('baseprice')"></h4>
                                   <div v-for="(item,index) in product.to_group.to_attr" :key="'esm'+index" class="form-group col-sm-12 col-xs-12">

                                       <label>{{ item.name }}</label>
                                       <template v-if="item.mode==1">
                                       <input @blur="textfea(item.id)" v-model="attr[item.id]" :ref="'fate'+item.id" class="form-control" type="text" >
                                   </template>
                                       <template v-if="item.mode==2">
                                           <input @blur="textfea(item.id)" v-model="attr[item.id]" :ref="'attr'+item.id" class="form-control" type="number" min="1" >
                                       </template>
                                       <template v-if="item.mode==3">
                                           <select  @blur="textfea(item.id)" v-model="attr[item.id]" :ref="'attr'+item.id" class="form-control" >
                                               <option value="1" v-text="$t('yes')"></option>
                                               <option value="0" v-text="$t('no')"></option>
                                           </select>
                                       </template>
                                       <template v-if="item.mode==4">
                                           <div :ref="'attr'+item.id" >
                                               <pre>{{ pricelist }}</pre>
                                               <template v-for="(opt,inx) in item.to_options"   >
                                                   <div   :key="'esma'+inx">
                                                       <div class="row">
                                                       <div class="col-sm-6 col-xs-12">
                                                           <div class="mychecker" dir="rtl">
                                                               <label>

                                                                   <input   :ref="'opt'+opt.id" v-model="optionattr[opt.id]"    :value="opt.id"  type="checkbox"  >
                                                                   <span class="checkmark"></span>
                                                                   <span v-text="opt.name"></span></label>
                                                           </div>
                                                           <input type="button" class="btn btn-primary" :value="$t('save')">
                                                       </div>
                                                       <div class="col-sm-6 col-xs-12">
                                                           <label v-text="$t('price')"></label>
                                                           <money dir="ltr"  class="form-control"  v-bind="money"></money>
                                                           <label v-text="$t('pricediscount')"></label>
                                                           <money dir="ltr"  class="form-control"  v-bind="money"></money>

                                                       </div>
                                                   </div>
                                                   <hr>
                                                   </div>
                                               </template>
                                           </div>
                                       </template>
                                       <hr>
                                   </div>

                                   </div>
                           </div>
                           <div id="menu3" class="container tab-pane fade"><br>
                               <h3 v-text="$t('feature')"></h3>
                               <hr>
                               <div class="container">
                                   <div v-for="(item,index) in product.to_group.to_feature" :key="'esmai'+index" class="form-group col-sm-12 col-xs-12">

                                       <label>{{ item.name }}</label>
                                       <template v-if="item.mode==1">

                                           <input @blur="textattr(item.id)" v-model="attr[item.id]" :ref="'attr'+item.id" class="form-control" type="text" >
                                       </template>
                                       <template v-if="item.mode==2">
                                           <input @blur="textattr(item.id)" v-model="attr[item.id]" :ref="'attr'+item.id" class="form-control" type="number" min="1" >
                                       </template>
                                       <template v-if="item.mode==3">
                                           <select  @blur="textattr(item.id)" v-model="attr[item.id]" :ref="'attr'+item.id" class="form-control" >
                                               <option value="1" v-text="$t('yes')"></option>
                                               <option value="0" v-text="$t('no')"></option>
                                           </select>
                                       </template>
                                       <template v-if="item.mode==4">
                                           <div :ref="'attr'+item.id" >
                                               <pre>{{ item.id }}</pre>

                                               <div v-for="(opt,inx) in item.to_options" :key="'esmail'+inx" class="mychecker" dir="rtl">
                                                   <label>
                                                       <pre style="color:#fff;">FUCK DAY {{ optionsattr[opt.id] }}</pre>

                                                       <input   :name="'opt'+opt.id"

                                                                @change="clickoptattr(opt.id,item.id,$event)"
                                                                type="checkbox"
                                                       >
                                                       <span class="checkmark"></span>
                                                       <span v-text="opt.name"></span></label>
                                               </div>
                                           </div>
                                       </template>
                                       <hr>
                                   </div>

                               </div>
                           </div>
                           <div id="review" class="container tab-pane fade"><br>

                               <h3 v-text="$t('review')"></h3>
                               <p>
                                   <tisseditor :key="'esmail'+2" :text="product.review" v-on:myevent="reviewedit"   :mode="'Product'"></tisseditor>
                               </p>
                               <h3 v-text="$t('description')"></h3>
                               <p>
                                   <tisseditor   :key="'esmails'+1"  :text="product.description" v-on:myevent="descriptionedit"   :mode="'Product'"></tisseditor>
                               </p>
                               <h3 v-text="$t('help')"></h3>
                               <p>
                                   <tisseditor  :key="'esmailso'+4"  :text="product.help" v-on:myevent="helpedit"   :mode="'Product'"></tisseditor>
                               </p>
                           </div>

                       </div>
                   </div>
                   <div class="col-sm-12">
                       <input type="submit" class="btn btn-primary" :value="$t('save')">
                   </div>
               </form>

           </template>
       </div>
        <pre>{{ product }}</pre>

        <showerror :errors="error"></showerror>
    </div>
</template>

<script>
    import Showerror from "../../Custom/Showerror";
    import Tisseditor from "../../Custom/Tisseditor";
    import FileUploader from "../../Custom/FileUploader";
    import VueTagsInput from '@johmun/vue-tags-input';

    import {Money} from 'v-money';

    export default {
        name: "productdetail.vue",
        components:{
            Showerror,
            Tisseditor,
            FileUploader,
            Money,
            VueTagsInput
        },
        data() {
            return {
                tags:[],
                tag:'',
                money: {
                    decimal: ',',
                    thousands: '.',
                    prefix: '',
                    suffix: '',
                    precision: 0,
                    masked: false
                },
                taglist:null,
                price:0,
                discount:0,
                mode:'edit',
                listcolor:[],
                pricelist:'',
                group:[],
                attr:[],
                coloredit:null,
                fea:[],
                optionsfea:[],
                optionattr:[],
                error:null,
                listitems:[],
                optionsattr:[],
                imagelist:[],
                product:{
                    id:null,
                    name:null,
                    url:null,
                    parent:null
                },
                status:{
                    0:this.$t('inactive'),
                    1:this.$t('active'),
                    2:this.$t('unavailable'),
                },
                special:{
                    0:this.$t('normal'),
                    1:this.$t('special'),

                },
                booleanarray:{
                    0:this.$t('no'),
                    1:this.$t('yes'),

                }

            }
        },

        watch: {
            product:function (data) {
                let that=this;
                    data.to_attr.filter(function (attr) {
                        if(attr.value=='options'){
                            attr.to_option_value.filter(function (opt){
                                if(opt.value!=0){
                                   // console.log(that.optionsattr[opt.attr])
                                   // that.optionsattr[opt.attr]=true;
                                    console.log('opt'+opt.attr);
                                    console.log(opt.value);
                                    console.log('Fucx');
                                    console.log(that.$refs);
                                    alert('opt'+opt.attr);
                                    that.opt.attr='yes';
                                    document.getElementsByName('opt14').checked=true;
                                    console.log(that.$refs['opt'+opt.attr][0]);
                                   // that.$refs['opt'+opt.attr][1]['checked']=true;
                                };

                            });
                        }else{
                            that.attr[attr.attr]=attr.value;
                        }
                    });
                    data.to_price.filter(function (attr) {
                        if(attr.attr==0){
                            that.price=attr.price;
                            that.discount=attr.discount;
                            that.percent=attr.percent;
                        }
                    })
            }
        },
        computed:{
            filteredItems() {
                return this.autocompleteItems.filter(i => {
                    return i.text.toLowerCase().indexOf(this.tag.toLowerCase()) !== -1;
                });
            },
            autocompleteItems(){
                let b=[];
                this.taglist.forEach(function (item) {
                    b.push({text:item.name});

                });
                return b;
            },
            taggenerator(){
                let b=[];
                this.product.to_tag.forEach(function(item){
                    b.push(item.name);
                });
                return b;
            },
        },

        methods:{
            colororderup(id){
                let self=this;
                this.$axios.get(this.$url+'user/colororderup/'+id,{
                    headers:{
                        Authorization: localStorage.token
                    }
                }).then(function (res) {
                    self.loadcolor();
                });
            },
            deletecolor(id){
              let self=this;
              this.$axios.delete(this.$url+'user/pcolor/'+id,{
                  headers:{
                      Authorization: localStorage.token
                  }
              }).then(function (res) {
                  self.loadcolor();
              });
            },
            colororderdown(id){
                let self=this;
                this.$axios.get(this.$url+'user/colororderdown/'+id,{

                    headers:{
                        Authorization: localStorage.token

                    }
                }).then(function (res) {
                    self.loadcolor();
                });
            },
            editcolor(id){
                this.coloredit=this.listcolor[id];
                console.log(this.coloredit);
                this.$forceUpdate();  // Notice we have to use a $ here
                this.$modal.show('hello-world');

            },
            addtocolorexist(color){
                let data= {
                    color: color,
                    id: this.product.id
                };
                let that=this;
                this.$axios.post(this.$url+'user/pcolor',data,{
                    headers: {
                        Authorization: localStorage.token
                    }
                }).then(function(res){
                    that.loadcolor();
                })
            },
            loadcolor(){
                let self=this;
                this.$axios.get(this.$url+'user/pcolor/'+this.product.id,{
                    headers:{
                        Authorization: localStorage.token

                    }
                }).then(function (res) {
                    self.listcolor=res.data;
                });

            },
            newpricesubmit(){
                let data={
                    id:this.product.id,
                    price:this.price,
                    discount:this.discount,
                    percent:this.percent,
                    attr:0,
                };
                this.$axios.post(this.$url+'user/pprice',data, {
                    headers: {
                        Authorization: localStorage.token
                    }
                });
            },
            // Attr Controller

            clickoptattr(id,parent,event){

                let data={
                    attr:parent,
                    options:id,
                    product:this.product.id
                };
               if(this.$refs['opt'+id][1]['checked']==true){
                    data.value=1;
                }else{
                   data.value=0;
               }

                this.$axios.post(this.$url+'user/popt',data, {
                    headers: {
                        Authorization: localStorage.token
                    }
                });
            },
            checkboxattr(id){
                console.log(this.attr[id]);
              /*  this.$refs['attr'+id][0]['children'].map(function (m) {
                    console.log(m);
                })*/
            },
            textfea(id){

        /*        let data={
                    id:id,
                    product:this.product.id,
                    value:this.$refs['attr'+id][0]['value']
                }
                this.$axios.post(this.$url+'user/pattr',data, {
                    headers: {
                        Authorization: localStorage.token
                    }
                });*/
            },
            textattr(id){

                    let data={
                        id:id,
                        product:this.product.id,
                        value:this.$refs['attr'+id][0]['value']
                    }
                this.$axios.post(this.$url+'user/pattr',data, {
                    headers: {
                        Authorization: localStorage.token
                    }
                });
            },
            // End Attr Controller
            iamgemanagers(e){
            this.coloredit.image=e;
            },
            savecolor(){
                let that=this;
              this.$axios.put(this.$url+'user/pcolor/'+this.product.id,this.coloredit,{
                  headers:{
                      Authorization: localStorage.token

                  }
              }) .then(function (res) {
              });
            },
            addpicture(e){
             let that=this;
             let data={
                 product:this.product.id,
                 image:e
             }
                
             this.$axios.post(this.$url+'user/pimage',data,{
                 headers: {
                     Authorization:localStorage.token
                 }
             }).then(function(res){
                that.loadimage();
             })
            },
            masterimg(id){
                let that=this;
                let data={

                };
                this.$axios.put(this.$url+'user/pimage/'+id,data,
                    {
                        headers:{
                            Authorization:localStorage.token
                        }
                    }).then(function (response) {
                    that.loadimage();

                });

            },
            delimage(id){
                let that=this;
              this.$axios.delete(this.$url+'user/pimage/'+id,{
                  headers:{
                      Authorization:localStorage.token

                  }
              }).then(function(res){
                  that.loadimage();
              });
            },
            loadimage(){
                let that=this;

                this.$axios.get(this.$url+'user/pimage',{
                    params:{
                      id:that.product.id
                    },
                    headers: {
                        Authorization:localStorage.token
                    }
                }).then(function(res){
                    that.imagelist=res.data;
                })
            },
            reviewedit(e){
                this.product.review=e;
            },
            morecommentedit(e){
                this.product.morecomment=e;
            },
            descriptionedit(e){
                this.product.description=e;
            },
            helpedit(e){
                this.product.help=e;
            },
            urlcreate(){
                if(this.product.id==null){
                    let str=this.product.name;
                    this.product.url=str.replace(/#| /g,'_');

                };
            },
            save(){
                let that=this;
                if(this.product.id==null){
                    this.$axios.post(this.$url+'user/pdetail',this.product,{
                        headers: {
                            Authorization:localStorage.token
                        }
                    }).then(function(res){
                        that.mode='edit';
                    })
                        .catch((error) => {
                            that.error = error.response.data.errors;

                        });
                }else{

                }
                if(this.product.id!=null){
                    this.product.tag=JSON.stringify(this.tags);

                    this.$axios.put(this.$url+'user/pdetail/'+this.product.id,this.product,{
                        headers: {
                            Authorization:localStorage.token
                        }
                    }).then(function(res){
                        that.$swal.fire(that.$t('Saved'));
                    })
                        .catch((error) => {
                            that.error = error.response.data.errors;

                        });
                }

            },
            resetform(){
                this.product={
                    id:null,
                        name:null,
                        url:null,
                        parent:null
                }
                this.price=null;
                this.discount=null;
                this.percent=null;
            },
            add(){
                this.resetform();
                this.mode='edit';

            },
            edit(id){
                let that=this;
                this.$axios.get(this.$url+'user/pdetail/'+id,{
                    headers: {
                        Authorization:localStorage.token
                    }

                }).then(function(res){
                    that.product=res.data;
                    that.imagelist=res.data.to_image;
                    that.tags=that.taggenerator;

                    that.mode='edit';
                 /**/
                });
            },
            listgroup(){

                let that=this;
                this.$axios.get(this.$url+'user/Tag',{
                    headers: {
                        Authorization:localStorage.token
                    }
                }).then(function(res){
                    that.taglist=res.data;
                });
                this.$axios.get(this.$url+'user/pgroup/create',{

                    headers: {
                        Authorization:localStorage.token
                    }
                }).then(function(res){
                    that.group=res.data;
                })
                    .catch((error) => {
                        that.error = error.response.data.errors;

                    });
            },
            listproduct(page='1',name='',group=''){
                this.resetform();
                this.mode='list';
                let that=this;
                this.$axios.get(this.$url+'user/pdetail',{
                    params:{
                        page: page,
                        name: name,
                        group: group,
                    },
                    headers: {
                        Authorization:localStorage.token
                    }
                }).then(function(res){
                    that.listitems=res.data;

                })
                    .catch((error) => {
                        that.error = error.response.data.errors;

                    });
            },
        },
        mounted() {
                this.mode='list';
                this.listgroup();
                this.listproduct();

        }
    }
</script>

<style scoped>

    /* The container */
    .mychecker {
        display: block;
        position: relative;
        padding-right: 35px;
        margin-bottom: 12px;
        cursor: pointer;
        font-size: 20px;
        -webkit-user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
        user-select: none;
        direction: rtl;
    }

    /* Hide the browser's default checkbox */
    .mychecker input {
        position: absolute;
        opacity: 0;
        cursor: pointer;
        height: 0;
        width: 0;
    }

    /* Create a custom checkbox */
    .checkmark {
        position: absolute;
        top: 0;
        right: 0;
        height: 25px;
        width: 25px;
        background-color: #eee;
    }

    /* On mouse-over, add a grey background color */
    .mychecker:hover input ~ .checkmark {
        background-color: #ccc;
    }

    /* When the checkbox is checked, add a blue background */
    .mychecker input:checked ~ .checkmark {
        background-color: #2196F3;
    }

    /* Create the checkmark/indicator (hidden when not checked) */
    .checkmark:after {
        content: "";
        position: absolute;
        display: none;
    }

    /* Show the checkmark when checked */
    .mychecker input:checked ~ .checkmark:after {
        display: block;
    }

    /* Style the checkmark/indicator */
    .mychecker .checkmark:after {
        left: 9px;
        top: 5px;
        width: 5px;
        height: 10px;
        border: solid white;
        border-width: 0 3px 3px 0;
        -webkit-transform: rotate(45deg);
        -ms-transform: rotate(45deg);
        transform: rotate(45deg);
    }
    .btncolor{
        display:inline-block;width: 10px; height: 10px; overflow: hidden;
        margin-right: 10px;
        margin-left: 10px;
        border-radius: 45px;
    }
    .mylistcolor li{
        list-style: none;
    }
</style>