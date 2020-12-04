<template>
  <Layout>
    <!-- Page Header -->
    <!-- <header class="masthead" style="background-image: url('img/home-bg.jpg')"> -->
    <header class="masthead" :style="'background-image: url('+api_url+$page.general.edges[0].node.cover.url+')'">
    
    <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="site-heading">
              <h1>{{$page.general.edges[0].node.title}}</h1>
              <span class="subheading">{{$page.general.edges[0].node.subtitle}}</span>
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Main Content -->
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto">
          <div class="post-preview" v-for="edge in $page.posts.edges" :key="edge.node.id">
            <g-link :to="'/post/'+edge.node.id">
              <h2 class="post-title">
                {{edge.node.title}}
              </h2>
            </g-link>
            <p class="post-meta"> 
              Publish on
              {{edge.node.created_at}}
            </p>
            <p class="post-meta">
              <g-link v-for="tag in edge.node.tags" :key="tag.id" :to="'/tag/'+tag.id">
                {{tag.title}} 
              </g-link>
            </p>
          <hr />

          </div>
          
    <Pager :info="$page.posts.pageInfo" class="post-meta"/>

        </div>
      </div>
      
    </div>

    <hr />
  </Layout>
</template>

<page-query>
query ($page: Int){
  posts: allStrapiPost(perPage:5,page:$page)@paginate{
    pageInfo {
        totalPages
        currentPage
      }
    edges {
      node {
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
  }

  general: allStrapiGeneral{
    edges {
      node {
        id
        title
        subtitle
        cover{
          url
        }
      }
    }
  }
}
</page-query>

<script>
import {Pager} from 'gridsome'

export default {
   components: {
    Pager
  },
  name:"Index",
  metaInfo: {
    title: "Index Page",
  },
};
</script>