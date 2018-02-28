<template>
  <article class="col-sm-12">
		<h1>{{ post.title }}</h1>		
		<p>{{ post.body }}</p>

		<nav aria-label="breadcrumb">
			<ol class="breadcrumb">
				<li class="breadcrumb-item"><router-link :to="'/'">Home</router-link></li>
				<li class="breadcrumb-item active" aria-current="page">{{ post.title }}</li>
			</ol>
		</nav>

		<h2>Discussion</h2>
		<button @click="showComments" v-if="!showCommentBox" class="btn btn-primary">show comments</button>

		<ul class="list-group" v-if="showCommentBox">
			<li v-for="comment in comments" class="list-group-item"><strong>{{ comment.email }}</strong> <em>wrote:</em> {{ comment.body }}</li>
		</ul>
  </article>
</template>

<script>
export default {
  data() {
    return {
      post: {},
	  	comments: [],
			showCommentBox: false,
    }
  },
  created() {
    this.$http.get("http://jsonplaceholder.typicode.com/posts/" + this.$route.params.id)
      .then(response => response.json(), error => console.log(error))
      .then(json => this.post = json, error => console.log(error));
  },
  methods: {
	  showComments(){
			this.$http.get("http://jsonplaceholder.typicode.com/comments?postId=" + this.$route.params.id)
      		.then(response => response.json(), error => console.log(error))
      		.then(json =>	this.comments = json, error => console.log(error))
					.then(() => this.showCommentBox = true);
	  }
  }

}
</script>

<style>

</style>
