<template>
  <div class="mainLayout">
    <Header />
    <div class="faLayout" v-if="$store.state.lang == 'fa'">
      <div class="bar faPage">
        <div class="barIcon" @click="openMenu">
          <div class="firstLine">
            <span></span>
          </div>
          <div class="secLine">
            <span></span>
          </div>
          <div class="thirdLine">
            <span></span>
          </div>
        </div>
        <img src="/images/enLogo.svg" class="enLogo" alt="" />
        <div class="langDiv">
          <div class="resLanguage">
            <img src="/icons/global.svg" alt="global" @click="handelLang" />
            <div class="effect">
              <div @click="changeToEn">EN</div>
              <div @click="changeToFa">FA</div>
            </div>
          </div>
        </div>
      </div>
      <Nuxt />
      <Footer />
    </div>
    <div class="enLayout enPage" v-if="$store.state.lang == 'en'">
      <div class="bar">
        <div class="barIcon" @click="openMenu">
          <div class="firstLine">
            <span></span>
          </div>
          <div class="secLine">
            <span></span>
          </div>
          <div class="thirdLine">
            <span></span>
          </div>
        </div>
        <img src="/images/enLogo.svg" class="enLogo" alt="" />
        <div class="langDiv">
          <div class="resLanguage">
            <img src="/icons/global.svg" alt="global" @click="handelLang" />
            <div class="effect">
              <div @click="changeToEn">EN</div>
              <div @click="changeToFa">FA</div>
            </div>
          </div>
        </div>
      </div>
      <Nuxt />
      <Footer />
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      headerOpen: false,
    };
  },
  mounted() {
    document.getElementsByClassName("resLanguage")[0].style.height = "26px";
    if (this.$route.path.split("/")[1] == "en") {
      this.$store.commit("changeToEn");
    } else {
      this.$store.commit("changeToFa");
    }
  },
  methods: {
    openMenu() {
      this.headerOpen = true;
      if (window.innerWidth > 719) {
        document.getElementsByClassName("faHeader")[0].style.transition =
          "transform 1s";
        document.getElementsByClassName("faHeader")[0].style.transform =
          "translateX(152px)";
        document.getElementsByClassName("faHeader")[0].style.padding = "0px";
        document.getElementsByClassName("menu")[0].style.display = "none";
        document.getElementsByClassName("langAndScroll")[0].style.display =
          "none";
        document.getElementsByClassName("openedMenu")[0].style.display = "flex";

        document.getElementsByClassName("enHeader")[0].style.transition =
          "transform 1s";
        document.getElementsByClassName("enHeader")[0].style.transform =
          "translateX(152px)";
        document.getElementsByClassName("enHeader")[0].style.padding = "0px";
        document.getElementsByClassName("menu")[1].style.display = "none";
        document.getElementsByClassName("langAndScroll")[1].style.display =
          "none";
        document.getElementsByClassName("openedMenu")[1].style.display = "flex";
      } else {
        document.getElementsByClassName("faHeader")[0].style.transition =
          "transform 1s";
        document.getElementsByClassName("faHeader")[0].style.transform =
          "translateX(0px)";
        document.getElementsByClassName("faHeader")[0].style.padding = "0px";
        document.getElementsByClassName("menu")[0].style.display = "none";
        document.getElementsByClassName("langAndScroll")[0].style.display =
          "none";
        document.getElementsByClassName("openedMenu")[0].style.display = "flex";

        document.getElementsByClassName("enHeader")[0].style.transition =
          "transform 1s";
        document.getElementsByClassName("enHeader")[0].style.transform =
          "translateX(0px)";
        document.getElementsByClassName("enHeader")[0].style.padding = "0px";
        document.getElementsByClassName("menu")[1].style.display = "none";
        document.getElementsByClassName("langAndScroll")[1].style.display =
          "none";
        document.getElementsByClassName("openedMenu")[1].style.display = "flex";
      }
    },
    handelLang() {
      const lang = document.getElementsByClassName("resLanguage")[0];
      if (lang.style.height == "26px") {
        lang.style.height = "140px";
      } else {
        lang.style.height = "26px";
      }
    },
    changeToEn() {
      this.$store.commit("changeToEn");
      const currentPath = this.$route.fullPath.replace("fa", "en");
      this.$router.push(currentPath);
    },
    changeToFa() {
      this.$store.commit("changeToFa");
      const currentPath = this.$route.fullPath.replace("en", "fa");
      this.$router.push(currentPath);
    },
  },
  watch: {
    "$route.path"() {
      if (this.$route.path.split("/")[1] == "en") {
        this.$store.commit("changeToEn");
      } else {
        this.$store.commit("changeToFa");
      }
    },
  },
};
</script>