<template>
  <div>
    <div>
      <mainHeader @changeDraw="changeDraw" />
    </div>

    <v-main>
      <v-container fluid>
        <transition
          appear
          enter-active-class="animated fadeIn"
          leave-active-class="animated fadeOut"
          :duration="600"
          mode="out-in"
        >
          <router-view></router-view>
        </transition>
      </v-container>
    </v-main>
    <mainFooter />
  </div>
</template>

<script>
import mainFooter from '../components/structure/mainFooter.vue';
import mainHeader from '../components/structure/mainHeader.vue';

export default {
  name: 'default',
  components: {
    mainFooter,
    mainHeader,
  },

  data() {
    return {
      drawer: '', // Hide mobile side menu by default
    };
  },

  methods: {
    changeDraw(value) {
      this.drawer = value;
    },
  },
};
</script>
<style lang="scss">
@import '../../node_modules/@aasaam/noto-font/dist/font-face.css';
// @import '~/scss/variable.scss';

$body-font-family: 'aasaam-Noto', sans-serif;

.v-application {
  font-family: $body-font-family;
  background: #fff !important;
}
.v-application .headline {
  font-family: $body-font-family !important;
  background: #fff !important;
}
a {
  text-decoration: none;
}
.sh-0 {
  box-shadow: none !important;
}
.fn13 {
  font-size: 13px;
}
.fn12 {
  font-size: 12px;
}
.clear {
  overflow: auto;
}
</style>
