<template>
  <Layout>
    <div class="container-inner mx-auto my-16">
      <h2 class="text-4xl font-bold mb-8 border-b">タグ: {{ $page.tag.title }}</h2>

      <div v-for="post in $page.tag.belongsTo.edges" :key="post.node.id" class="post border-gray-400 border-b mb-12">
        <!-- 言語毎に表示を分ける -->
        <div v-if="post.node.language === $context.locale">
          <h2 class="text-3xl font-bold">
          <g-link :to="$context.locale + '/' + post.node.path" class="text-copy-primary">{{ post.node.title }}</g-link>
          </h2>
          <div class="text-copy-secondary mb-4">
            <span>{{ post.node.date }}</span>
            <span> &middot; </span>
            <!--<span>{{ post.node.timeToRead }} min read</span>-->
            <span>{{ post.node.language }}</span>
          </div>

          <div class="text-lg mb-4">
            {{ post.node.summary }}
          </div>

          <div class="mb-8">
            <g-link :to="$context.locale + '/' + post.node.path" class="font-bold uppercase">{{ $t('read more') }}３</g-link>
          </div>
        </div>
      </div>

      <pagination-posts
        v-if="$page.tag.belongsTo.pageInfo.totalPages > 1"
        :base="`/tag/${$page.tag.title}`"
        :totalPages="$page.tag.belongsTo.pageInfo.totalPages"
        :currentPage="$page.tag.belongsTo.pageInfo.currentPage"
      />

    </div>
  </Layout>
</template>

<page-query>
query Tag ($id: ID!, $page: Int) {
  tag: tag (id: $id) {
    title
    belongsTo (page: $page, perPage: 3) @paginate {
      totalCount
      pageInfo {
        totalPages
        currentPage
      }
      edges {
        node {
          ...on Post {
            title
            language
    	      date (format: "Y/MM/D")
            path
            summary
            tags {
              title
            }
          }
        }
      }
    }
  }
}
</page-query>

<script>
import PaginationPosts from '../components/PaginationPosts'

export default {
  metaInfo() {
    return {
      title: 'Tag: ' + this.$page.tag.title
    }
  },
  components: {
    PaginationPosts
  }
}
</script>
