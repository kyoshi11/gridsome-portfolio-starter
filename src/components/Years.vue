<template>
  <div>
    <div
      v-for="(year, yindex) in new Set(
        $static.years.edges.map((e) => e.node.year)
      )"
      :key="`y-${yindex}`"
    >
      <h6>
        » {{ year }}
      </h6>
      <div>
        <g-link
          v-for="(month, mindex) in new Set(
            $static.years.edges
              .map((e) => e.node.month)
              .filter((e) => e.indexOf(year) === 0)
              .reverse()
          )"
          :key="`m-${mindex}`"
          :to="`/archives/date/${month}`"
          >{{ month.slice(-2) }}</g-link
        >
        <g-link
          :to="`/archives/date/${year}`"
          >all</g-link
        >
      </div>
    </div>
  </div>
</template>

<static-query>
query {
  years: allPost(sortBy: "published_at", order: ASC) {
    edges { 
      node { 
        year: date(format: "YYYY")
        month: date(format: "YYYY/MM")
      }
    }
  }
}
</static-query>