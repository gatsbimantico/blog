<template>
  <Layout>
    <div class="project">

      <g-image :src="$page.post.thumbnail" height="567px" blur="40" quality="50" />

      <div class="project-header-anchor">
        <div class="project-header">
          <h1 class="project-title" v-html="$page.post.title" />
          <div class="project-info">

            <div class="categories-container">
              <div class="categories">
                <span class="label">Categories</span>
                <span
                  class="category"
                  v-for="(category, index) in $page.post.categories"
                  :key="index"
                  v-text="category"
                />
              </div>
            </div>

            <div class="year-container">
              <span class="label">Year</span>
              <div v-html="$page.post.date"/>
            </div>
          </div>
        </div>
      </div>
      <div class="container">

        <div v-html="$page.post.content" class="content" />

      </div>
        <h2 class="project-subtitle">Project journal</h2>
        <g-link
          :to="post.node.path"
          v-for="post in posts"
          :key="post.node.id"
          class="journal-post"
        >
          <div class="container journal">
            <h2 class="journal-title">{{ post.node.title }}</h2>
            <p class="journal-excerpt">{{ post.node.excerpt }}</p>
          </div>
        </g-link>

      </div>

  </Layout>
</template>

<page-query>
query ProjectPost ($path: String!) {
  post: projectPost (path: $path) {
    title
    thumbnail (height:567, quality: 50)
    date (format: "YYYY")
    content
    categories
    journal
    project_bg_color
    project_fg_color
  }
	posts: allJournalPost {
    edges {
      node {
        id
        path
        title
        excerpt
      }
    }
  }
}
</page-query>

<script>
export default {
  data() {
    return {
      posts: [],
    };
  },
  mounted() {
    this.posts = this.$page.posts.edges
      .filter(edge => this.$page.post.journal.includes(`${edge.node.path.replace(/^\//, '')}.md`));
  },
  metaInfo () {
    return {
      title: this.$page.post.title,
      bodyAttrs: {
        style: `background-color: ${this.$page.post.project_bg_color ? this.$page.post.project_bg_color : 'var(--color-base)'}; color: ${this.$page.post.project_fg_color ? this.$page.post.project_fg_color : 'var(--color-contrast)'}`
      }
    }
  }
}
</script>

<style scoped>
.project-header-anchor {
  position: relative;
}
.project-header {
  padding: 10px 0 10px;
}
@media (min-width: 800px) {
  .project-header {
    padding: 0 0 10px;
    position: absolute;
    transform: translateY(-100%);
    background: rgba(255, 255, 255, 0.85);
    border: 2px solid rgb(0, 0, 0);
    top: -14px;
    left: 11px;
  }
}

.project-header {
}
.project-title {
  font-size: 3rem;
  margin: 0 0 10px 0;
  padding: 0 0.7rem;
  display: inline-block;
}
.project-subtitle {
  padding: 0 0.7rem;
}
.project-info {
  display: flex;
  flex-wrap: wrap;
  font-size: 0.8rem;
}
.project-info > div {
  margin-right: 4rem;
}
.project-info > div:last-of-type {
  margin: 0;
}
.category:after {
  content: ', '
}
.category:last-of-type:after {
  content: '';
}
.categories-container,
.year-container {
  padding: 0.3rem 0.7rem;
}
.container.journal {
  max-width: 720px;
}
.journal-post {
  display: block;
  padding: 2rem 0;
  text-decoration: none;
  transition: background 0.5s ease;
}
.journal-post > * {
  transition: transform 0.5s ease;
}
.journal-post:hover {
  background-color: var(--color-base-1);
}
.journal-post:hover > * {
  transform: translateX(4rem);
}
.journal-post h1,
.journal-post h2 {
  margin: 0;
  padding: 0;
}
.journal-title {
  font-size: 2rem;
  color: var(--color-contrast);
}
.journal-excerpt {
  color: var(--color-contrast-1);
}
</style>
