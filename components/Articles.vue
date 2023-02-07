<template>
  <section class='container mt-5'>
    <HeadingBrush
      :content='headingBrushContent'
      headingType="h2"
    />
    <div v-if="articles.length" class="row mt-5">
      <aside class="col-lg-3 mt-4">
        <div class="card">
          <div class="card-body">
            <h5 class="card-title text-center">Categorias</h5>
            <ul class="nav flex-column">
              <li class="nav-item">
                <button
                  class="btn btn-transparent"
                  :class="{active: !categorySelected}"
                  @click="selectCategory(null)"
                >Todo</button>
              </li>
              <li v-for="category of categories" class="nav-item">
                <button
                  class="btn btn-transparent"
                  :class="{active: categorySelected === category}"
                  @click="selectCategory(category)"
                >{{category}}</button>
              </li>
            </ul>
          </div>
        </div>
      </aside>
      <section class="col-lg-9 mx-auto row">
        <article v-for="article of articles" class="col-md-6 col-lg-4 px-0 d-flex">
          <div class="card mx-md-1 mx-lg-3 mt-4">
            <img class="card-img-top" :src="article.image" alt="Card image cap">
            <div class="card-body">
              <a :href="article.url"><h5 class="card-title">{{article.title}}</h5></a>
              <p class="card-text">{{article.content}}</p>
              <a :href="article.url">Leer mas</a>
            </div>
          </div>
        </article>
      </section>
    </div>
  </section>
</template>

<script>

const API_URL = 'https://5eed24da4cbc340016330f0d.mockapi.io/api/articles'

export default {
  name: 'Articles',
  data: () => ({
    articles: [],
    categories: [],
    categorySelected: null,
    loading: false,
    error: ''
  }),
  async fetch() {
    this.articles = await fetch(API_URL).then(res => res.json())
    // extract categories from articles and insert into categories array
    this.categories = this.articles.reduce((categories, article) => {
      if (!categories.includes(article.category)) {
        return categories.concat(article.category)
      }
      return categories
    }, [])
  },
  computed: {
    headingBrushContent() {
      if (this.$fetchState.pending || this.loading) {
        return 'Cargando articulos...'
      }
      if (this.$fetchState.error || this.error) {
        console.log($fetchState.error)
        return 'Error cargando articulos'
      }
      return 'Nuestros articulos'
    }
  },
  methods: {
    selectCategory: async function(category) {
      this.articles = []
      this.categorySelected = category
      this.loading = true
      this.error = ''
      let newURL = API_URL
      if (category) {
        newURL = `${newURL}?filter=${category}`
      }
      try {
        this.articles = await fetch(newURL).then(res => res.json());
      } catch(err) {
        this.error = 'No se pudieron cargar los articulos'
      } finally {
        this.loading = false
      }
    }
  }
}
</script>

<style scoped>
  button.active {
    color: #D8AD3D;
  }
  button:focus {
    box-shadow: none;
  }
  .card:hover a {
    color: #D8AD3D;
  }
</style>
