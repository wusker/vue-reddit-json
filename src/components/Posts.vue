<template>
  <div>
    <h1>Posts</h1>
    <ul>
      <li v-for="(post, index) in posts" v-bind:key="index">
        <img :src="post.data.thumbnail" :alt="post.data.title" />
        <h3>
          <a :href="createUrl(post.data.permalink)" target="_blank">{{post.data.title}}</a>
        </h3>
        <small>Comments: {{post.data.num_comments}}</small>
        <span>{{post.data.ups}}</span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Posts",
  data() {
    return {
      posts: []
    };
  },
  mounted() {
    this.load();
  },
  methods: {
    load() {
      const cors = "https://cors-anywhere.herokuapp.com/";
      const url = `${cors}https://www.reddit.com/r/rarepuppers/.json`;
      fetch(url)
        .then(response => response.json())
        .then(result => {
          this.posts = result.data.children;
          console.log(this.posts);
        })
        .then(() =>
          this.posts.forEach((post, index) => {
            if (post.data.thumbnail === "self") {
              this.posts.splice(index, 2);
            }
          })
        )
        .catch(err => console.log(err));
    },
    createUrl(path) {
      return `https://www.reddit.com/${path}`;
    }
  }
};
</script>

<style scoped>
h1 {
  margin: 3vw;
  text-align: center;
  font-size: 2rem;
}
ul {
  margin-right: 5vw;
}
li {
  background: rgba(30, 45, 55, 0.619);
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  margin-bottom: 3vw;
  color: white;
  padding: 2vw;
  position: relative;
  flex-wrap: wrap;
  border-radius: 2px;
}
li h3 {
  font-size: 1.5rem;
  flex-basis: 100%;
}
li small {
  background: rgb(58, 78, 87);
  color: white;
  border-radius: 50px;
  padding: 0.25rem 0.6rem;
}
li img {
  border-radius: 2px;
  height: 100%;
  flex-basis: 80%;
}
li span {
  color: rgb(246, 255, 144);
  font-size: 1.5rem;
  position: absolute;
  top: 2vw;
  right: 2vw;
}
li a {
  cursor: pointer;
  color: rgb(188, 255, 154);
  text-decoration: none;
}
li a:hover {
  color: rgb(255, 169, 104);
}
</style>
