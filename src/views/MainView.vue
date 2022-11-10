<template>
  <div>
    <HeaderCont />
    <section class="main__cont">
      <div class="main__inner container">
        <div v-for="title in title" v-bind:key="title.text">
          {{ title.text }}
        </div>
      </div>
    </section>
    <FooterCont />
  </div>
</template>

<script>
import HeaderCont from "@/components/HeaderCont.vue";
import FooterCont from "@/components/FooterCont.vue";

export default {
  components: {
    HeaderCont,
    FooterCont,
  },
  data: function () {
    return {
      title: [
        { text: "we provide" },
        { text: "visual coding" },
        { text: "solution" },
        { text: "for you API" },
      ],
    };
  },
};
</script>

<style lang="scss">
.main__inner {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  flex-direction: column;
  height: 100vh;
  color: var(--white);

  > div {
    font-size: 8vw;
    line-height: 1;
    text-transform: uppercase;
    color: #000;
  }
}
</style>
