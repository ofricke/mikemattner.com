<template>
  <article :class="['single-link', archive == true ? 'article--link' : '']">
    <nuxt-link :to="`/${formatSlug(article.attributes.title)}`">
      <div class="article-meta">
        <time>{{ formatDate(article.attributes.date) }}</time>
      </div>
      <Header tag="h3" class="article-title display-6">{{
        article.attributes.title
      }}</Header>
      <!-- <p class="article-description">{{ article.attributes.description }}</p> -->
    </nuxt-link>
  </article>
</template>

<script>
export default {
  props: {
    article: {
      type: Object,
      required: true
    },
    archive: Boolean
  },
  methods: {
    formatDate(date) {
      return new Date(date).toDateString().slice(4)
    },
    formatExcerpt(body) {
      return body.slice(0, 200).trimEnd()
    },
    formatSlug(title) {
      const regex = / /gi
      return title
        .toLowerCase()
        .trim()
        .replace(regex, '-')
    }
  }
}
</script>

<style lang="scss">
.single-link {
  display: block;
  // padding: 2rem 3rem 2rem 0;
  background-image: none;
  position: relative;
  overflow: hidden;
  // @media (min-width: $tablet) {
  //   padding: 1.5rem 0;
  // }
  a {
    display: flex;
    justify-content: flex-start;
    align-items: center;
    background-image: none;
    background-position: 0% 100%;
    background-repeat: no-repeat;
    background-size: 0 0;
    padding: 1.5rem 0.25rem;
    border-bottom: 1px solid rgba($white, 0.05);
  }
  h3 {
    transition: $transition;
    font-size: 1rem;
    margin: 0;
    transition: all 0.25s ease-in-out;
    color: $white;
  }
  &:hover {
    background-color: $darkBlue-1;
    h3 {
      transform: translateX(20px);
      color: $primary;
      font-style: italic;
    }
    .article-meta {
      color: $primary;
    }
  }
  &.article--link {
    width: 100%;
    a {
      width: 100%;
    }
  }
  .article-description {
    margin-left: 2rem;
    font-size: $small;
  }
  .article-title {
    margin: 0;
  }
  .article-meta {
    font-size: $small;
    margin: 0 0.25rem 0 0;
    flex: 0 0 100px;
    text-transform: uppercase;
    color: rgba($white, 0.5);
    transition: $transition;
  }
}
</style>
