<template>
  <Layout>
    <div class="container">
      <div class="breadcrumbs">
        <ol itemscope itemtype="https://schema.org/BreadcrumbList">
          <li itemprop="itemListElement" itemscope
              itemtype="https://schema.org/ListItem">
            <g-link to="/" itemprop="item" :itemid="`${hostname}`">
              <span itemprop="name">Home</span>
              <meta itemprop="position" content="1">
            </g-link>
          </li>
          <li itemprop="itemListElement" itemscope
              itemtype="https://schema.org/ListItem">
            <g-link to="/portfolio/"
                    itemprop="item"
                    :itemid="`${hostname}/portfolio/`">
              <span itemprop="name">Portfolio</span>
              <meta itemprop="position" content="2">
            </g-link>
          </li>
          <li itemprop="itemListElement" itemscope
              itemtype="https://schema.org/ListItem">
            <span itemprop="name">Websites</span>
            <meta itemprop="position" content="3">
          </li>
        </ol>
      </div>
      <h1 class="highlight-overline">Website Projects</h1>
      <h2>Websites</h2>
      <div class="cards">
        <card v-for="item in $page.website_projects.edges"
              :key="item.id"
              :image="item.node.image">
            <h3>{{ item.node.title }}</h3>
            <p class="description">{{ item.node.description }}</p>
            <g-link :to="item.node.path" class="button small">View</g-link>
        </card>
      </div>

    </div>
  </Layout>
</template>

<page-query>
query {
  website_projects: allProject (filter: { category: { eq: "website" } }, sortBy: "order", order: ASC) {
    edges {
      node {
        id
        title
        description
        image
        path
        order
      }
    }
  }
}
</page-query>


<script>
import Card from '@/components/Card'
export default {
  name: 'Website',
  metaInfo: {
    title: 'Website Projects - Portfolio',
    meta: [{
      key: 'description',
      name: 'description',
      content: 'A selection of fast, responsive website projects, including static sites, content management systems and PWA\'s'
    }],
    link: [
      {
        key: 'canonical',
        rel: 'canonical',
        href: `${process.env.GRIDSOME_HOSTNAME}/portfolio/website/`
      }
    ],
  },
  components: { Card },
  data () {
    return {
      hostname: process.env.GRIDSOME_HOSTNAME
    }
  }
}
</script>
