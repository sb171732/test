<template>
      <div class="container" v-cloak>
         
       <el-card>
             <h2>{{ $route.params.news.title  }}</h2>
             <h4 class="mt">{{ $route.params.news.pubDate }} 
             <p class="mt" v-if="$route.params.news.author!=''">
                 Автор: {{ $route.params.news.author  }} </p> </h4>
             <p class="mt mb" v-html="$route.params.news.description"></p>

              <el-row>
                  <el-col :span="8" v-for="(m,i) in Array.of($route.params.news.enclosure)" :key="i">
                       <el-image 
                        style=""
                        :src="m.link" 
                        :preview-src-list="[m.link]">
                       </el-image>
                  </el-col>
              </el-row>
              <el-link class="mt" :href="$route.params.news.link" target="_blank">Ссылка на источник</el-link>
       </el-card>
      </div>
</template>
<script>
export default {}
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