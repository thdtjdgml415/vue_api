<template>
  <div>
    <HeaderCont />
    <TitleCont name1="unsplash" name2="reference" />
    <section class="cont__refer">
      <div class="container">
        <div class="unsplash__inner">
          <h2>unsplash</h2>
          <div class="unsplash__sldier"></div>
          <div class="unsplash__search"></div>
          <div class="unsplash__images">
            <ul>
              <li v-for="splash in splashes" :key="splash.id">
                <a href="#">
                  <img :src="splash.urls.regular" :alt="splash.id" />
                </a>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </section>
    <ContactCont />
    <FooterCont />
  </div>
</template>

<script>
import HeaderCont from "@/components/HeaderCont.vue";
import TitleCont from "@/components/TitleCont.vue";
import FooterCont from "@/components/FooterCont.vue";
import ContactCont from "@/components/ContactCont.vue";
import { ref } from "vue";
export default {
  components: {
    HeaderCont,
    TitleCont,
    ContactCont,
    FooterCont,
  },

  setup() {
    const splashes = ref([]);
    const search = ref("space");

    const SearchSplashes = () => {
      // fetch(
      //   `https://api.unsplash.com/search/photos?page=1&query=${search.value}&client_id=Z4A0XicGRKz2GK0TTtsrNqvywI8vODnxiGoNDoUhc34&per_page=20&count=30&language=ko`
      // )
      //   .then((response) => response.json())
      //   .then((result) => console.log(result))
      //   .then((error) => console.log(error));
    };
    SearchSplashes();
    const RandomSplashes = () => {
      fetch(
        "https://api.unsplash.com/photos/random?client_id=Z4A0XicGRKz2GK0TTtsrNqvywI8vODnxiGoNDoUhc34&count=30"
      )
        .then((response) => response.json())
        .then((result) => (splashes.value = result))
        // .then((result) => console.log(result))
        .then((error) => console.log(error));
    };
    RandomSplashes();

    return {
      splashes,
      search,
      // SearchSplashes,
      RandomSplashes,
    };
  },
};
</script>

<style lang="scss">
.unsplash__images {
  width: 100%;
  ul {
    width: 100%;
    li {
      display: inline-block;
      width: 20%;
      margin: 10px;
    }
    img {
      width: 100%;
    }
  }
}
</style>
