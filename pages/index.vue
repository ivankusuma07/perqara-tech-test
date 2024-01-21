<template>
  <div class="page-wrapper mt-20 z-0 absolute top-0">
    <div class="wrapper-discover">
      <div class="z-50">
        <div class="grey-bg -z-10">
          <div class="m-[7.5rem] pt-[89px]">
            <div class="red-line mb-[12px]"></div>
            <div class="flex justify-between">
              <div class="text-2xl font-semibold text-[#E5E5E5]">Discover Movies</div>
              <div>
                <button :class="`btn ${pops} mr-2`" @click="clickBtnPopularity()">
                  Popularity
                </button>
                <button :class="`btn ${release}`" @click="clickBtnReleaseDate()">
                  Release Date
                </button>
              </div>
            </div>
          </div>
        </div>
        <div
          class="flex flex-row flex-wrap justify-center gap-10 fade-slow relative z-50 -mt-36"
        >
          <client-only>
            <div v-for="movie in listMovie" :key="movie.id">
              <div class="card-wrapper">
                <div class="overlay flex flex-col justify-center gap-10">
                  <div class="flex flex-row justify-center">
                    <img src="~/assets/img/star.svg" alt="star" class="mr-2" />
                    <span class="inline-block text-2xl font-bold text-[#E5E5E5]">
                      {{ movie.vote_average }}
                    </span>
                  </div>
                  <div class="text-[#E5E5E5] text-center text-wrap">
                    {{ filterGenre(movie.genre_ids) }}
                  </div>
                  <div class="flex justify-center">
                    <button :class="`btn active`">
                      <NuxtLink :to="`detail/${movie.id}`"> View </NuxtLink>
                    </button>
                  </div>
                </div>
                <div
                  class="relative top-8 left-[10.8rem] bg-[#1E232BCC] text-[#E5E5E5] w-[48px] h-[32px] text-lg font-bold text-center"
                >
                  {{ movie.vote_average }}
                </div>
                <img
                  v-if="movie.poster_path !== null"
                  :src="`https://image.tmdb.org/t/p/original/${movie.poster_path}`"
                  width="220"
                  height="330"
                  alt=""
                />
                <img
                  v-else
                  src="https://files.prokerala.com/movies/assets/img/no-poster-available.jpg"
                  width="220"
                  height="330"
                  alt="No poster available"
                />
                <div class="mt-[13px] font-semibold text-base text-[#E5E5E5]">
                  {{ movie.title }}
                </div>
                <div class="mt-[3px] font-normal text-sm text-[#929292]">
                  {{ movie.release_date.slice(0, 4) }}
                </div>
              </div>
            </div>
          </client-only>
        </div>
      </div>
    </div>
    <!-- </div> -->
    <Footer />
  </div>
</template>
<script lang="ts" setup>
definePageMeta({
  layout: 'default',
})
// const classBtn = ref('')
const pops = ref('active')
const release = ref('')
const listMovie = ref([])
const sortBy = ref('popularity.desc')
const clickBtnPopularity = () => {
  release.value = ''
  pops.value = 'active'
  sortBy.value = 'popularity.desc'
  getMovieList()
}
const clickBtnReleaseDate = () => {
  release.value = 'active'
  pops.value = ''
  sortBy.value = 'primary_release_date.desc'
  getMovieList()
}

const listGenre = [
  {
    id: 28,
    name: 'Action',
  },
  {
    id: 12,
    name: 'Adventure',
  },
  {
    id: 16,
    name: 'Animation',
  },
  {
    id: 35,
    name: 'Comedy',
  },
  {
    id: 80,
    name: 'Crime',
  },
  {
    id: 99,
    name: 'Documentary',
  },
  {
    id: 18,
    name: 'Drama',
  },
  {
    id: 10751,
    name: 'Family',
  },
  {
    id: 14,
    name: 'Fantasy',
  },
  {
    id: 36,
    name: 'History',
  },
  {
    id: 27,
    name: 'Horror',
  },
  {
    id: 10402,
    name: 'Music',
  },
  {
    id: 9648,
    name: 'Mystery',
  },
  {
    id: 10749,
    name: 'Romance',
  },
  {
    id: 878,
    name: 'Science Fiction',
  },
  {
    id: 10770,
    name: 'TV Movie',
  },
  {
    id: 53,
    name: 'Thriller',
  },
  {
    id: 10752,
    name: 'War',
  },
  {
    id: 37,
    name: 'Western',
  },
]

const filterGenre = (data: Array<{}>) => {
  // console.log(data)
  const filteredGenre = listGenre.filter((item) => {
    return data.includes(item.id)
  })

  const names = filteredGenre.map(function (item) {
    return item['name']
  })

  return names.slice(0, -1).join(', ') + ', ' + names.at(-1) + ''
}

const getMovieList = async () => {
  const options = {
    method: 'GET',
    headers: {
      accept: 'application/json',
      Authorization:
        'Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiI0MjY3ZWE5ZjVlMDBjNTgyMzQxN2IxMDk4ZmI1YTM2OSIsInN1YiI6IjY1YWEyNGI4N2NhYTQ3MDEyYjA5NjhmOCIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.BvNPwYCOx7H87JF9NMefAG0iMpGmVpyImF_imaf5FMU',
    },
  }

  const { data: movie, refresh } = await useFetch(
    `https://api.themoviedb.org/3/discover/movie?include_adult=false&include_video=false&language=en-US&page=1&sort_by=${sortBy.value}`,
    {
      method: 'GET',
      headers: {
        accept: 'application/json',
        Authorization:
          'Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiI0MjY3ZWE5ZjVlMDBjNTgyMzQxN2IxMDk4ZmI1YTM2OSIsInN1YiI6IjY1YWEyNGI4N2NhYTQ3MDEyYjA5NjhmOCIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.BvNPwYCOx7H87JF9NMefAG0iMpGmVpyImF_imaf5FMU',
      },
    }
  )
  listMovie.value = movie.value.results ?? []
  console.log(movie.value)
  watchEffect(() => {
    refresh()
  })
  //   .then(response => response.json())
  //   .then(response => console.log(response))
  //   .catch(err => console.error(err));)

  // fetch('https://api.themoviedb.org/3/discover/movie?include_adult=false&include_video=false&language=en-US&page=1&sort_by=popularity.desc', options)
  //   .then(response => response.json())
  //   .then(response => console.log(response))
  //   .catch(err => console.error(err));
}

getMovieList()
</script>
<style lang="postcss" scoped>
.wrapper-discover {
  @apply h-auto mb-32;
}

.card-wrapper {
  @apply relative text-wrap max-w-[220px] h-auto;
}

.card-wrapper:hover .overlay {
  opacity: 1;
}

.overlay {
  position: absolute;
  top: 32px;
  bottom: 0;
  left: 0;
  right: 0;
  height: auto;
  width: 100%;
  opacity: 0;
  transition: 0.5s ease;
  background-color: #000000cc;
}

.grey-bg {
  @apply bg-[#FFFFFF0D] h-[333px] relative z-10;
}

.btn {
  @apply bg-[#00000033] h-[32px] rounded-[32px] w-auto text-[#E5E5E5] text-sm font-semibold px-2;
}

.active {
  @apply bg-[#F00];
}
.btn:hover {
  @apply bg-[#0000007b];
}
.red-line {
  @apply w-[112px] h-[6px] bg-[#E74C3C];
}
.page-wrapper {
  position: relative; /* for the footer to move with the page size */
  min-height: 100%; /* for the footer to be at the bottom */
  padding-bottom: 6rem;
}
.bg-greyblack {
  background: #1e232b;
}
.badge {
  @apply inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700;
  &:hover {
    @apply bg-gray-300;
  }
}
</style>
