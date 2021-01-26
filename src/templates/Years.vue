<!-- ./src/templates/Years.vue -->
<template>
  <Layout>
    <div>
      <h1 class="entry-title" itemprop="headline">
        {{ $context.displayYear }}
      </h1>

      <ul>
        <li v-for="{ node } in $page.years.edges" :key="node.id">
          <g-link :to="node.path">
            <span v-html="node.title" />
          </g-link>
          {{ node.date }}
        </li>
      </ul>
    </div>
  </Layout>
</template>

<!-- periodStartDateとperiodEndDateの範囲内にある記事を検索する -->
<page-query>
query PostsByDate($periodStartDate: Date, $periodEndDate: Date) {
  years: allPost(filter: {date: {between: [$periodStartDate, $periodEndDate]} }) {
    edges {
      node {
        id
        title
        path
        date(format: "YYYY/MM/DD")
      }
    }
  }
}
</page-query>