<template>
  <div>
    <HeaderCont />
    <TitleCont name1="reference" name2="api" />
    <section class="cont__refer">
      <div class="container">
        <div class="refer__inner">
          <h2>CSS</h2>
          <ul class="refer__list">
            <li v-for="refer in refers" :key="refer.title">
              <a href="#">
                <span class="num">{{ refer.num }}</span>
                <span class="title">{{ refer.title }}</span>
                <span class="descApply">{{ refer.descApply }}</span>
                <span class="descStar">{{ refer.descStar }}</span>
              </a>
            </li>
          </ul>
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
import ContactCont from "@/components/ContactCont.vue";
import FooterCont from "@/components/FooterCont.vue";
import { ref } from "vue";

export default {
  components: {
    HeaderCont,
    TitleCont,
    ContactCont,
    FooterCont,
  },

  setup() {
    const refers = ref([]);

    const references = () => {
      fetch("http://thdtjdgml415.github.io/react_api/src/utils/reference.json")
        .then((response) => response.json())
        .then((result) => (refers.value = result.cssRefer))
        // .then((result) => console.log(result))
        .catch((error) => console.log("error", error));
    };
    references();

    return {
      refers,
      references,
    };
  },
};
</script>

<style lang="scss">
.refer__list {
  border: 1px solid var(--bg-dark-border);
  li {
    border-bottom: 1px solid var(--bg-dark-border);
    a {
      display: flex;
      width: 100%;
      color: var(--white);
      align-items: center;

      span {
        display: inline-block;
      }
      .num {
        flex: 1 1 5%;
        text-align: center;
        border-right: 1px solid var(--bg-dark-border);
      }
      .name {
        flex: 1 1 20%;
        border-right: 1px solid var(--bg-dark-border);
      }
      .desc {
        flex: 1 1 65%;
        border-right: 1px solid var(--bg-dark-border);
      }
      .star {
        flex: 1 1 19%;
        text-align: center;
        display: flex;
      }
    }
  }
}
</style>
