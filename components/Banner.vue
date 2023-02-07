<template>
  <header class="container-fluid px-0 wrapper">
    <!-- NAVBAR -->
    <div class="container">
      <nav class="navbar navbar-expand-lg navbar-light bg-transparent">
        <a class="navbar-brand" href="#">Logo</a>
        <div class="collapse navbar-collapse mt-2" id="navbar-top">
          <ul class="navbar-nav ml-auto">
            <li class="nav-item mr-2">
              <SocialLink
                :icon="socials.facebook.icon"
                :url="socials.facebook.url"
                color="#009CD9"
              />
            </li>
            <li class="nav-item mr-2">
              <SocialLink
                :icon="socials.instagram.icon"
                :url="socials.instagram.url"
                color="#B72C2C"
              />
            </li>
            <li class="nav-item">
              <SocialLink
                :icon="socials.youtube.icon"
                :url="socials.youtube.url"
                color="#D8AD3D"
              />
            </li>
          </ul>
        </div>
      </nav>

      <!-- CONTENT HERO SECTION -->
      <section class="hero d-flex align-items-center">
        <h1>El secreto <br /> de tu cocina</h1>
      </section>
    </div>
  </header>
</template>

<script>

export default {
  name: 'Banner',
  data: function(){
    return {
      socials: {
        facebook: {
          icon: 'icons/facebook-f.svg',
          url: '#'
        },
        instagram: {
          icon: 'icons/instagram.svg',
          url: '#'
        },
        youtube: {
          icon: 'icons/youtube.svg',
          url: '#'
        }
      }
    }
  }
}
</script>

<style scoped>
  .hero {
    min-height: 70vh;
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
</style>
