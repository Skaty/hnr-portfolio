<template>
  <a :href="getPortfolio" class="card">
    <img class="card-img" :src="require(`../img/${themePic}`)">
    <div class="card-section">
      <h4>{{ themeName }}</h4>
    </div>
    <div class="card__color" :class="color">
    </div>
  </a>
</template>

<script>
export default {
  name: 'theme-card',
  props: {
    githubId: String,
    themeName: String,
    themePic: String,
    themeId: Number,
  },
  computed: {
    // eslint-disable-next-line
    color: function() {
      return `card__color--${(this.themeId % 3) + 1}`;
    },
    // eslint-disable-next-line
    getPortfolio: function() {
      if (this.githubId) {
        return `page/${this.githubId}/${this.themeId}`;
      }
      return '/';
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.card {
  display: block;
  position: relative;
  height: 10rem;
  transition: opacity 0.35s, transform 0.35s;
  transform: scale3d(1.05, 1.05, 1);
  cursor: pointer;
}

.card:hover {
  opacity: 0.7;
  transform: scale3d(1, 1, 1);
}

.card::before {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(255,255,255,0.7);
  content: '';
  transition: transform 0.6s;
  transform: scale3d(1.9,1.4,1) rotate3d(0,0,1,45deg) translate3d(0,-150%,0);
}

.card:hover::before {
  transform: scale3d(1.9,1.4,1) rotate3d(0,0,1,45deg) translate3d(0,100%,0);
}

.card:hover .card__color {
  opacity: 0;
}

.card-img {
  position: absolute;
  z-index: -1;
  left: 0;
  top: 0;
}

.card-section {
  display: flex;
  justify-content: center;
  align-content: center;
  height: 100%;
  transition: opacity 0.35s, transform 0.35s;
  transform: translatey(0.5rem);
  opacity: 0;
}

.card-section > h4 {
  margin: auto;
}

.card-section:hover {
  opacity: 1;
  transform: translatey(0);
}
</style>
