<template>
<transition appear>
  <div id="app" class="hero">
    <section>
      <div class="row header">
        <h1 class="columns small-12">Gitfolio</h1>
        <div class="columns small-12">Amazing portfolios, at a click of your fingers</div>
      </div>
    </section>
    <section class="hero__header" :class="{ 'hero__header--initial': !isGithubId }">
      <h3 class="instruction instruction--lower" :class="{ text: !isGithubId }">Github username</h3>
      <div class="row">
        <div class="columns small-12 medium-8 large-6 small-centered username">
          <div class="username__text" :class="{ text: !isGithubId }">https://github.com/</div>
          <div class="username__link">
            <label>
              <input v-model="githubId" v-on:keyup="delay" class="username__input" type="text" placeholder="li-kai">
            </label>
          </div>
        </div>
      </div>
    </section>
    <transition name="fade">
    <main v-show="isGithubId">
      <h3 class="instruction instruction--higher">Pick a theme</h3>
      <ul class="row small-up-1 medium-up-3 large-up-4 theme-list">
        <li class="column column-block" v-for="(pic, name, index) in themes">
          <p-theme-card :github-id="githubId" :theme-name="name" :theme-pic="pic" :theme-id="index"></p-theme-card>
        </li>
      </ul>
    </main>
    </transition>
  </div>
</transition>
</template>

<script>
import throttle from 'lodash.throttle';
import PThemeCard from './components/ThemeCard';
import themes from './assets/themes.json';

export default {
  name: 'app',
  components: {
    PThemeCard,
  },
  methods: {
    // eslint-disable-next-line
    delay: throttle(function() {
      if (Boolean(this.isGithubId) !== Boolean(this.githubId)) {
        this.isGithubId = this.githubId;
      }
    }, 200),
  },
  // eslint-disable-next-line
  data: function() {
    return {
      themes,
      githubId: '',
      isGithubId: false,
    };
  },
};
</script>

<style lang="scss">
$body-font-family: 'Raleway', Helvetica, Arial, sans-serif;
$transition-timing: 0.4s;
@import '~foundation-sites/scss/foundation';
@include foundation-everything;

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.hero {
  height: 100%;
  min-height: 100vh;
  background-size:cover;
  background-image: url("./img/stock-2.jpg");
}

.header {
  padding-top: 1rem;
}

.hero__header {
  margin-top: 1rem;
  transition: transform $transition-timing ease-out, color $transition-timing ease-out;
}

.hero__header--initial {
  transform: translateY(20vh);
}

.instruction {
  margin-bottom: 0;
}

.instruction--lower {
  margin-bottom: -0.7rem;
}

.instruction--higher {
  margin-bottom: 0.7rem;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity $transition-timing ease-out, transform $transition-timing ease-out;
}
.fade-enter, .fade-leave-to /* .fade-leave-active in <2.1.8 */ {
  transform: translateY(5rem);
  opacity: 0
}

.theme-list {
  list-style: none;
}

.username {
  margin-top: 1rem;
  margin-bottom: 1rem;
  display: flex;
  align-items: center;
  justify-content: center;
}

.username__text {
  margin-right: 0.2rem;
  text-align: right;
}

.text {
  color: white;
}

@media (min-width: 768px) {
  .text {
    color: inherit;
  }
}

.username__input {
  margin: 0;
}
</style>
