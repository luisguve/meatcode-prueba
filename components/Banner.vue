<template>
  <header class="container-fluid px-0 wrapper">
    <!-- NAVBAR -->
    <div class="container">
      <nav class="navbar navbar-expand-lg navbar-light bg-transparent">
        <a class="navbar-brand font-primary" href="#">Logo</a>
        <div class="collapse navbar-collapse mt-2" id="navbar-top">
          <ul class="navbar-nav ml-auto">
            <li v-for="social of socials" class="nav-item mr-2">
              <a class="nav-link" :href="social.url">
                <SocialLink
                  :icon="social.icon"
                  :color="social.color"
                  :ariaLabel="social.ariaLabel"
                />
              </a>
            </li>
          </ul>
        </div>
      </nav>
      <!-- CONTENT HERO SECTION -->
      <section class="hero d-flex align-items-center">
        <h1 class="font-primary">El secreto <br /> de tu cocina</h1>
      </section>
    </div>
  </header>
</template>

<script>

export default {
  name: 'Banner',
  data: function(){
    return {
      socials: [
        {
          icon: 'icons/facebook-f.svg',
          url: '#',
          color: '#009CD9',
          ariaLabel: 'Facebook page'
        },
        {
          icon: 'icons/instagram.svg',
          url: '#',
          color: '#B72C2C',
          ariaLabel: 'Instagram page'
        },
        {
          icon: 'icons/youtube.svg',
          url: '#',
          color: '#D8AD3D',
          ariaLabel: 'YouTube channel'
        }
      ]
    }
  }
}
</script>

<style scoped>
  .hero {
    min-height: 70vh;
  }
  .hero h1 {
    font-size: 125px;
    line-height: 0.85;
  }
  .navbar-brand {
    font-size: 55px;
  }
  .wrapper {
    background: url(/hero.webp);
    background-repeat: no-repeat;
    background-position-y: center;
    background-position-x: right;
    background-size: cover;
    position: relative;
  }
  .wrapper::before {
    content: "";
    position: absolute;
    z-index: 1;
    top: 0;
    left: -20%;
    width: 75%;
    height: 100%;
    background: url("/brush.webp");
    background-repeat: no-repeat;
    background-position-y: 91%;
    background-position-x: center;
    background-size: 115%;
  }
  .wrapper h1 {
    z-index: 100;
  }
  @media screen and (max-width: 768px) {
    .hero h1 {
      font-size: 75px;
    }
    .navbar-brand {
      font-size: 35px;
    }
  }
</style>
