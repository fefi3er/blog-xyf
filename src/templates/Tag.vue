<template>
  <Layout>
    <!-- Page Header -->
    <header class="masthead" :style="'background-image: url(https://xyfcms.applinzi.com'+$page.posts.posts[0].image.url+')'">
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="site-heading">
              <h1>{{$page.posts.title}}</h1>
              <span class="subheading">A Tag for Posts</span>
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Main Content -->
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto">
          <div class="post-preview" v-for="edge in $page.posts.posts" :key="edge.id">
            <g-link :to="'/post/'+edge.id">
              <h2 class="post-title">
                {{edge.title}}
              </h2>
            </g-link>
            <p class="post-meta">
              Publish on
              {{edge.created_at}}
            </p>
          <hr />

          </div>
          

        </div>
      </div>
      
    </div>

    <hr />
  </Layout>
</template>

<page-query>
query ($id: ID!){
  posts: strapiTag(id:$id){
        id
        title
        posts{
          id 
          title
          created_at
          image{
            url
          }
        }
      }
}
</page-query>

<script>

export default {
  name:"Tag",
  metaInfo: {
    title: "Tag Page",
  },
};
</script>