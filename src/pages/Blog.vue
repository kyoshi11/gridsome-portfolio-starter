<template>
  <Layout>
    <div class="container-inner mx-auto py-16">
      <div v-for="post in $page.posts.edges" :key="post.id" class="post border-gray-400 border-b mb-12">
        <div>post={{ post.language }} post_node={{ post.node.language }}</div>
      　<div v-if="post.language=ja">
          <h2 class="text-3xl font-bold"><g-link :to="post.node.path" class="text-copy-primary">{{ post.node.title }} おお</g-link></h2>
          <div class="text-copy-secondary mb-4">
            <span>{{ post.node.date }}</span>
            <span> &middot; </span>
            <!-- <span>{{ post.node.timeToRead }} {{ $t('min read') }}</span> -->
            <span>{{ post.node.thumbnail }}</span>
          </div>

          <div class="text-lg mb-4">
            {{ post.node.summary }}
          </div>

          <div class="mb-8">
            <g-link :to="post.node.path" class="font-bold uppercase">{{ $t('read more') }}１</g-link>
          </div>
        </div>
      </div> <!-- end post -->

      <pagination-posts
        v-if="$page.posts.pageInfo.totalPages > 1"
        base="/blog"
        :totalPages="$page.posts.pageInfo.totalPages"
        :currentPage="$page.posts.pageInfo.currentPage"
      />
    </div>
  </Layout>
</template>

<page-query>
query Posts ($page: Int) {
  posts: allPost (sortBy: "date", order: DESC, perPage: 3, page: $page) @paginate {
    totalCount
    pageInfo {
      totalPages
      currentPage
    }
    edges {
      node {
        id
        title
        language
        date (format: "MMMM D, Y")
        summary
        thumbnail
        timeToRead
        path
      }
    }
  }
}
</page-query>

<script>
import PaginationPosts from '../components/PaginationPosts'

export default {
  metaInfo: {
    title: 'Blog'
  },
  components: {
    PaginationPosts
  }
}
</script>

