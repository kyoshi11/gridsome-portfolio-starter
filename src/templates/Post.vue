<template>
  <Layout>
    <div class="container-inner mx-auto my-16">
      <h1 class="text-4xl font-bold leading-tight">{{ $page.post.title }} normal</h1>
      <div :aa="$context.locale">Current locale: {{ $context.locale }}</div>
      <div :aa="$i18n.locale">i18:::{{ this.$i18n.locale }}</div>
      <div class="mb-8">lang::{{ $page.post.language}}</div>
      <div :bb="$route.path">path:::{{ this.$route.path }}</div>
      <div class="text-xl text-gray-600 mb-4">{{ $page.post.date }}</div>
      <div class="flex mb-8 text-sm">
        <g-link
          :to="$context.locale  + '/' + tag.path"
          v-for="tag in $page.post.tags"
          :key="tag.id"
          class="bg-gray-300 rounded-full px-4 py-2 mr-4 hover:bg-green-300">
          {{ tag.title }}
        </g-link>
      </div>
      <div class="markdown-body mb-8" v-html="$page.post.thumbnail" />
      <div class="markdown-body mb-8" v-html="$page.post.content" />
      <div class="mb-8">
        <g-link :to="$context.locale + '/blog'" class="font-bold uppercase">{{ $t('back to blog') }}</g-link>
        <!-- <g-link to="/blog" class="font-bold uppercase">{{ $t('back to blog') }}</g-link> -->
      </div>
    </div>
  </Layout>
</template>

<page-query>
query Post ($path: String!) {
  post: post (path: $path) {
    title
    language
    date (format: "Y/MM/D")
    thumbnail
    content
    tags {
      title
      path
    }
  }
}
</page-query>

<script>

export default {
  metaInfo() {
    return {
      title: this.$page.post.title
    }
  }
}
</script>

<style src="../css/github-markdown.css" />

