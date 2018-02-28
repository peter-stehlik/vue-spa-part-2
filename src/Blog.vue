<template>
  <div class="col-sm-12">
    <paginate
      name="blogs"
      :list="posts"
      :per="10"
      tag="div"
    >
      <section v-for="blog in paginated('blogs')">
        <h2>{{ blog.title }}</h2>
        <router-link :to="'/post/' + blog.id" class="btn btn-primary">read more</router-link>
        <hr>
      </section>
    </paginate>

    <paginate-links
      for="blogs"
      :async="true"
      :show-step-links="true"
      :step-links="{
        next: 'Next',
        prev: 'Previous'
      }"
      :classes="{
        'ul': 'pagination',
        'ul > li': 'page-item',
        'ul > li > a': 'page-link',
      }"  
    >
    </paginate-links>
  </div>
</template>

<script>
export default {
  data () {
    return {
      posts: [],
      paginate: ['blogs']
    }
  },
  created(){
    this.$http.get("http://jsonplaceholder.typicode.com/posts")
      .then(response => response.json(), error => console.log(error))
      .then(json => this.posts = json, error => console.log(error));
  }
}
</script>

<style>
  
</style>
