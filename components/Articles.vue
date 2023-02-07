<template>
  <section class='container mt-5'>
    <HeadingBrush content='Nuestros articulos' />
    <p v-if="$fetchState.pending">Cargando articulos...</p>
    <p v-else-if="$fetchState.error">Error cargando articulos: {{JSON.stringify($fetchState.error)}}</p>
    <div v-else class="row mt-5">
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
      <section class="col-lg-9 row">
        <article v-for="article of filteredArticles" class="col-lg-4 px-0 d-flex">
          <div class="card mx-3 mt-4">
            <img class="card-img-top" :src="article.image" alt="Card image cap">
            <div class="card-body">
              <a :href="article.url"><h5 class="card-title">{{article.title}}</h5></a>
              <p class="card-text">{{article.content}}</p>
            </div>
          </div>
        </article>
      </section>
    </div>
  </section>
</template>

<script>

const API_URL = 'https://5eed24da4cbc340016330f0d.mockapi.io/api/articles'

const dummyData = [{"id":1,"createdAt":"2020-06-20T07:38:19.965Z","title":"Tasty Cotton Tuna","category":"Recetas","image":"https://loremflickr.com/540/400/food?random=1","content":"Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean pulvinar risus at turpis.","url":"https://camila.biz"},{"id":2,"createdAt":"2020-06-20T01:16:49.346Z","title":"Handcrafted Plastic Towels","category":"Productos","image":"https://loremflickr.com/540/400/food?random=2","content":"Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean pulvinar risus at turpis.","url":"http://cary.net"},{"id":3,"createdAt":"2020-06-20T00:11:24.612Z","title":"Gorgeous Soft Keyboard","category":"Recetas","image":"https://loremflickr.com/540/400/food?random=3","content":"Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean pulvinar risus at turpis.","url":"https://olaf.biz"},{"id":4,"createdAt":"2020-06-20T08:24:27.700Z","title":"Ergonomic Soft Gloves","category":"Consejos","image":"https://loremflickr.com/540/400/food?random=4","content":"Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean pulvinar risus at turpis.","url":"https://ethan.name"},{"id":5,"createdAt":"2020-06-20T15:07:56.410Z","title":"Incredible Fresh Soap","category":"Consejos","image":"https://loremflickr.com/540/400/food?random=5","content":"Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean pulvinar risus at turpis.","url":"http://waldo.name"},{"id":6,"createdAt":"2020-06-20T08:41:31.722Z","title":"Unbranded Metal Pizza","category":"Recetas","image":"https://loremflickr.com/540/400/food?random=6","content":"Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean pulvinar risus at turpis.","url":"http://johnathan.biz"},{"id":7,"createdAt":"2020-06-20T13:10:52.485Z","title":"Refined Steel Cheese","category":"Productos","image":"https://loremflickr.com/540/400/food?random=7","content":"Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean pulvinar risus at turpis.","url":"https://dangelo.org"},{"id":8,"createdAt":"2020-06-20T12:38:06.539Z","title":"Handmade Metal Soap","category":"Productos","image":"https://loremflickr.com/540/400/food?random=8","content":"Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean pulvinar risus at turpis.","url":"https://mac.name"},{"id":9,"createdAt":"2020-06-20T05:57:37.558Z","title":"Gorgeous Wooden Keyboard","category":"Productos","image":"https://loremflickr.com/540/400/food?random=9","content":"Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean pulvinar risus at turpis.","url":"https://grayce.org"},{"id":10,"createdAt":"2020-06-20T15:16:34.797Z","title":"Sleek Steel Shoes","category":"Consejos","image":"https://loremflickr.com/540/400/food?random=10","content":"Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean pulvinar risus at turpis.","url":"http://francesco.biz"},{"id":11,"createdAt":"2020-06-20T13:30:58.151Z","title":"Unbranded Granite Soap","category":"Recetas","image":"https://loremflickr.com/540/400/food?random=11","content":"Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean pulvinar risus at turpis.","url":"http://xavier.biz"},{"id":12,"createdAt":"2020-06-20T06:01:42.066Z","title":"Awesome Wooden Bike","category":"Productos","image":"https://loremflickr.com/540/400/food?random=12","content":"Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean pulvinar risus at turpis.","url":"http://jarred.com"},{"id":13,"createdAt":"2020-06-19T22:44:43.956Z","title":"Sleek Metal Fish","category":"Consejos","image":"https://loremflickr.com/540/400/food?random=13","content":"Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean pulvinar risus at turpis.","url":"http://fernando.biz"},{"id":14,"createdAt":"2020-06-20T08:14:01.334Z","title":"Fantastic Cotton Car","category":"Recetas","image":"https://loremflickr.com/540/400/food?random=14","content":"Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean pulvinar risus at turpis.","url":"https://general.biz"},{"id":15,"createdAt":"2020-06-20T10:44:40.235Z","title":"Gorgeous Plastic Pizza","category":"Recetas","image":"https://loremflickr.com/540/400/food?random=15","content":"Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean pulvinar risus at turpis.","url":"http://peyton.com"},{"id":16,"createdAt":"2020-06-20T05:29:21.192Z","title":"Generic Concrete Soap","category":"Productos","image":"https://loremflickr.com/540/400/food?random=16","content":"Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean pulvinar risus at turpis.","url":"http://devyn.biz"},{"id":17,"createdAt":"2020-06-20T04:43:24.511Z","title":"Unbranded Frozen Ball","category":"Consejos","image":"https://loremflickr.com/540/400/food?random=17","content":"Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean pulvinar risus at turpis.","url":"https://tyrique.biz"},{"id":18,"createdAt":"2020-06-20T17:52:32.338Z","title":"Licensed Rubber Sausages","category":"Consejos","image":"https://loremflickr.com/540/400/food?random=18","content":"Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean pulvinar risus at turpis.","url":"http://abigale.com"},{"id":19,"createdAt":"2020-06-19T21:46:13.043Z","title":"Licensed Granite Shirt","category":"Recetas","image":"https://loremflickr.com/540/400/food?random=19","content":"Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean pulvinar risus at turpis.","url":"https://hilbert.org"},{"id":20,"createdAt":"2020-06-20T17:07:12.619Z","title":"Incredible Granite Keyboard","category":"Productos","image":"https://loremflickr.com/540/400/food?random=20","content":"Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean pulvinar risus at turpis.","url":"https://annetta.biz"}]

export default {
  name: 'Articles',
  data: () => ({
    articles: [],
    categorySelected: null,
  }),
  async fetch() {
    // this.articles = await fetch(API_URL).then(res => res.json())
    this.articles = await new Promise(
      resolve => {
        setTimeout(() => {
          resolve(dummyData);
        }, 1000)
      }
    )
  },
  computed: {
    categories() {
      if (!this.articles.length) {
        return []
      }
      return this.articles.reduce((categories, article) => {
        if (!categories.includes(article.category)) {
          return categories.concat(article.category);
        }
        return categories;
      }, [])
    },
    filteredArticles() {
      const { categorySelected } = this;
      if (!categorySelected) {
        return this.articles;
      }

      return this.articles.filter(article => article.category === categorySelected);
    }
  },
  methods: {
    selectCategory: function(category) {
      this.categorySelected = category;
    }
  }
}
</script>

<style scoped>
  button.active {
    color: #D8AD3D;
  }
</style>
