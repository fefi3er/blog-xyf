<template>
  <Layout>
        <!-- Page Header -->
  <header class="masthead" :style="'background-image: url('+api_url+$page.post.image.url+')'">
    <div class="overlay"></div>
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto">
          <div class="post-heading">
            <h1>{{$page.post.title}}</h1>
            <h2 class="subheading"></h2>
            <span class="meta">Publish on 
              {{$page.post.created_at}}</span>
          </div>
        </div>
      </div>
    </div>
  </header> 

  <!-- Post Content -->
  <article>
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto" v-html="mdToHtml($page.post.content)">
   
        </div>
      </div>
    </div>
  </article>
  </Layout>
</template>

<page-query>
query ($id: ID!){
  post: strapiPost(id:$id){
  
        id
        title
        content
        image{
          url
        }
        tags{
          id 
          title
        }
        created_at
      }
    
}
</page-query>

<script>
import markdown from 'markdown-it'
const md = new markdown()

export default {
    name:'Post',
    metaInfo: {
      title: "Post Page",
    },
    methods:{
      mdToHtml(text){
        return md.render(text)
      }
    }
}
</script>

<style>

</style>