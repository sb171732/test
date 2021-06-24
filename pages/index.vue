<template>
  <div class="container" v-cloak>
    <div>
     
     <el-row style="margin-bottom:20px;margin-top:10px">

       <el-col :span="12" >
            <el-date-picker
              v-model="value1"
              type="date"
              placeholder="Фильтр по дате">
            </el-date-picker>
       </el-col>
       <el-col :span="12" style="">
            <el-input
              v-model="value2"
              placeholder="Фильтр по заголовку">
            </el-input>
       </el-col>
     </el-row>

     <el-row>
       
       <el-col  class="">
         
          <el-card v-for="(item,i) in fnews" :key="i" class="mb">
            
            <h4 v-html="item.pubDate"></h4>
            <h3 v-html="item.title"></h3>
            <p v-html="item.description"></p>
            <el-button class="mt" @click="check(item)">Подробнее ..</el-button>
          </el-card>
       </el-col>
       
     </el-row>
     
    </div>
  </div>
</template>

<script>
export default {
   data() {
     return{
        value1:'',
        value2:'',
        date:'',
        items: [],
        fitems: [],
        feed: "https://api.rss2json.com/v1/api.json?rss_url="+"http://static.feed.rbc.ru/rbc/logical/footer/news.rss"
     }
    },
   created: function() {
        this.fetchData();
    },
    methods: {
        fetchData() {
             this.$http.get(this.feed).then(response => {
                this.items = response.body.items;
            });
        },
        check(i){
            console.log(i.pubDate)
            this.$router.push({name:'newsview',params:{news:i}})
        }
        
    },
   computed:{
     fnews(){
        return this.items
        .filter( (n)=>{  return n.title.match(this.value2) }) 
        .filter( (n)=>{  return n.pubDate.match(this.date) }) 
      }
        
   },
    watch:{
      value1(to){
       
        let m =  to.getMonth();
        m = m + 1;
        if (m < 10){ m = '0' + m  }
        let d =  to.getDate();
        if (d < 10){ d = '0' + d  } 
        this.date = to.getFullYear()+'-'+m+'-'+d;
        

      }
    }
  }    
    
  

</script>

<style>
 .container{
   padding: 15px;
 }
 .mb{
    margin-bottom: 10px;
 }
 .mt{
   margin-top: 10px;
 }

</style>
