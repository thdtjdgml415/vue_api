<template>
  <div>
    <HeaderCont />
    <TitleCont name1="Movie" name2="api" />
    <section class="cont__refer">
      <div class="container">
        <div class="movie__inner">
          <div class="movie__slider">
            <swiper
              :effect="'coverflow'"
              :grabCursor="true"
              :centeredSlides="true"
              :autoplay="{
                delay: 2500,
                disableOnInteraction: false,
              }"
              :slidesPerView="'auto'"
              :initialSlide="5"
              :coverflowEffect="{
                rotate: 50,
                stretch: 0,
                depth: 100,
                modifier: 1,
                slideShadows: fales,
              }"
              :pagination="{
                clickable: true,
              }"
              :modules="modules"
              class="mySwiper"
            >
              <swiper-slide v-for="(slider, index) in sliders" :key="slider.id">
                <a :href="`https://image.tmdb.org/movie/${slider.id}`">
                  <img
                    :src="`https://image.tmdb.org/t/p/w500/${slider.poster_path}`"
                    :alt="slider.title"
                  />
                  <em>
                    <span class="rank">{{ index }}</span>
                    <span class="title">{{ slider.title }}</span>
                    <span class="star">{{ slider.vote_average }}</span>
                  </em>
                </a>
              </swiper-slide>
            </swiper>
          </div>
          <div class="movie__search">
            <div className="container">
              <h2>검색하기</h2>
              <form @submit.prevent="SearchMovies()">
                <input
                  type="search"
                  placeholder="검색하십쇼"
                  v-model="search"
                />
                <button type="submit">검색</button>
              </form>
            </div>
          </div>
          <div class="movie__movies">
            <div class="container">
              <div class="movie__list">
                <ul>
                  <li v-for="movie in movies" :key="movie.id">
                    <a :href="`https://image.tmdb.org/movie/${movie.id}`">
                      <img
                        :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`"
                        :alt="movie.title"
                      />
                      <em>
                        <span class="title">{{ movie.title }}</span>
                        <span class="star">{{ movie.vote_average }}</span>
                      </em>
                    </a>
                  </li>
                </ul>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <FooterCont />
    <ContactCont />
  </div>
</template>
<script>
import HeaderCont from "@/components/HeaderCont.vue";
import TitleCont from "@/components/TitleCont.vue";
import FooterCont from "@/components/FooterCont.vue";
import ContactCont from "@/components/ContactCont.vue";
import { ref } from "vue";
import { Swiper, SwiperSlide } from "swiper/vue";
import "swiper/css";
import "swiper/css/effect-coverflow";
import "swiper/css/pagination";
import { Autoplay, EffectCoverflow, Pagination } from "swiper";
export default {
  components: {
    HeaderCont,
    FooterCont,
    TitleCont,
    ContactCont,
    Swiper,
    SwiperSlide,
  },
  setup() {
    const movies = ref([]);
    const sliders = ref([]);
    const search = ref("마블");
    const SearchMovies = async () => {
      await fetch(
        `https://api.themoviedb.org/3/search/movie?api_key=0466376d0c5ab578b755f58c7beec394&language=en-US&page=1&include_adult=false&query=${search.value}`
      )
        .then((response) => response.json())
        .then((result) => {
          movies.value = result.results;
          search.value = "";
        })
        .catch((error) => console.log(error));
    };
    SearchMovies();
    const TopMovies = async () => {
      await fetch(
        "https://api.themoviedb.org/3/movie/popular?api_key=0466376d0c5ab578b755f58c7beec394&language=en-US&page=1"
      )
        .then((response) => response.json())
        .then((result) => (sliders.value = result.results))
        .catch((error) => console.log(error));
    };
    TopMovies();
    return {
      movies,
      sliders,
      search,
      SearchMovies,
      TopMovies,
      modules: [Autoplay, EffectCoverflow, Pagination],
    };
  },
};
</script>
<style lang="scss">
.movie__pop {
  width: 100%;
  overflow-x: auto;
  .movie__popname {
    color: snow;
    font-size: 25px;
    margin: 0 auto;
    width: fit-content;
    margin-bottom: 20px;
    text-decoration: underline;
    text-underline-position: under;
  }
  ul {
    display: flex;
    justify-content: space-between;
    width: 100%;
    margin: 0 auto;
    .swiper-wrapper {
      width: 32%;
      .swiper-slide-active img {
        border: 4px solid #fff;
        filter: brightness(140%);
      }
    }
    li {
      width: 30%;
      position: relative;
    }
    em {
      display: block;
      height: 80px;
      margin-bottom: 30px;
      font-family: var(--font-kor);
    }
    .title {
      padding: 5px 0;
      display: inline-block;
    }
    .star {
      background: #fff;
      color: #000;
      position: absolute;
      left: 10px;
      top: 10px;
      width: 30px;
      height: 30px;
      border-radius: 50%;
      text-align: center;
      line-height: 30px;
      font-weight: 700;
    }
  }
  a {
    color: var(--white);
  }
}
.movie__inner {
  ul {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    li {
      width: 23%;
      position: relative;
      em {
        display: block;
        height: 80px;
        margin-bottom: 30px;
        font-family: var(--font-kor);
      }
      .title {
        padding: 5px 0;
        display: inline-block;
        color: var(--black);
      }
      .star {
        background: #fff;
        color: #000;
        position: absolute;
        left: 10px;
        top: 10px;
        width: 30px;
        height: 30px;
        border-radius: 50%;
        text-align: center;
        line-height: 30px;
        font-weight: 700;
      }
    }
  }
  a {
    color: var(--white);
  }
}
.movie__search {
  margin-bottom: 100px;
  .container {
    position: relative;
  }
  h2 {
    color: var(--white);
    font-size: 40px;
    text-indent: -9999px;
    height: 0;
  }
  input {
    background: #000;
    border: 1px solid var(--white);
    border-radius: 50px;
    color: #fff;
    width: 100%;
    padding: 12px 30px;
    font-family: var(--font-kor1);
  }
  button {
    position: absolute;
    right: 3px;
    top: 5px;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    border: 0;
    font-family: var(--font-kor1);
    cursor: pointer;
    z-index: 1000;
    background: #000;
    &:hover {
      background: var(--white);
    }
  }
}
.movie__slider {
  .swiper-slide {
    width: 25%;
  }
  .swiper-wrapper {
    margin-bottom: 60px;
    .swiper-slide-active img {
      border: 4px solid var(--black);
      filter: brightness(140%);
    }
  }
  em {
    display: block;
    // height: 80px;
    // margin-bottom: 30px;
    font-family: var(--font-kor);
    .rank {
      color: #fff;
      position: absolute;
      right: 10px;
      top: 0;
      font-size: 30px;
    }
  }
  .title {
    padding: 5px 0;
    display: inline-block;
    color: #000;
    font-weight: bold;
  }
  .star {
    background: #fff;
    color: #000;
    position: absolute;
    left: 10px;
    top: 10px;
    width: 30px;
    height: 30px;
    border-radius: 50%;
    text-align: center;
    line-height: 30px;
    font-weight: 700;
  }
}
</style>
