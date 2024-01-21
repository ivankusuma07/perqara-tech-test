<template>
  <div>
    <client-only>
      <div class="page-wrapper absolute top-0 z-0">
        <div class="relative z-1">
          <img
            :src="`https://image.tmdb.org/t/p/original/${listMovie.backdrop_path}`"
            width="100%"
            height="100%"
            alt=""
            style="filter: brightness(0.3)"
          />
        </div>
        <div class="-mt-[500px]">
          <div class="score-bg z-2"></div>
          <div class="overview-bg z-2"></div>

          <div class="relative ml-[124px] flex flex-row z-[1000] gap-5 -mt-[730px]">
            <div>
              <img
                :src="`https://image.tmdb.org/t/p/original/${listMovie.poster_path}`"
                width="220"
                height="330"
                alt=""
              />
            </div>
            <div class="p-5">
              <div class="flex flex-col">
                <div class="text-lg font-medium text-[#FFFFFF]">
                  {{ getYear(listMovie.release_date) }}
                </div>
                <div class="text-4xl font-semibold text-[#E5E5E5]">
                  {{ listMovie.title }}
                </div>
                <div class="text-sm font-medium text-[#FFFFFF]">
                  {{ filterGenre(listMovie.genres ? listMovie.genres : []) }}
                </div>
              </div>
              <div class="mt-14">
                <div class="flex flex-row gap-5">
                  <div class="flex flex-row">
                    <img src="~/assets/img/star.svg" alt="star" class="mr-2" />
                    <span class="inline-block text-2xl font-bold text-[#E5E5E5]">
                      {{
                        listMovie.vote_average ? listMovie.vote_average.toFixed(1) : '0.0'
                      }}
                    </span>
                  </div>
                  <div class="border-r border-[#FFFFFF33]">
                    <div class="text-[#FFFFFF80] font-medium text-xs mr-[33px]">
                      USER SCORE
                    </div>
                    <div class="text-[#FFFFFF] font-medium text-xs uppercase">
                      {{ listMovie.status }}
                    </div>
                  </div>
                  <div class="border-r border-[#FFFFFF33]">
                    <div class="text-[#FFFFFF80] font-medium text-xs">STATUS</div>
                    <div class="text-[#FFFFFF] font-medium text-xs mr-[33px]">
                      {{
                        filterGenre(
                          listMovie.spoken_languages ? listMovie.spoken_languages : []
                        )
                      }}
                    </div>
                  </div>
                  <div class="border-r border-[#FFFFFF33]">
                    <div class="text-[#FFFFFF80] font-medium text-xs mr-[33px]">
                      LANGUAGE
                    </div>
                    <div class="text-[#FFFFFF] font-medium text-xs">
                      {{ listMovie.vote_count }}
                    </div>
                  </div>
                  <div class="border-r border-[#FFFFFF33]">
                    <div class="text-[#FFFFFF80] font-medium text-xs mr-[33px]">
                      BUDGET
                    </div>
                    <div class="text-[#FFFFFF] font-medium text-xs mr-[33px]">
                      {{ formatCurrency(listMovie.budget) }}
                    </div>
                  </div>
                  <div class="border-r border-[#FFFFFF33]">
                    <div class="text-[#FFFFFF80] font-medium text-xs">PRODUCTION</div>
                    <div class="text-[#FFFFFF] font-medium text-xs mr-[33px]">
                      {{
                        filterGenre(
                          listMovie.production_companies
                            ? listMovie.production_companies
                            : []
                        )
                      }}
                    </div>
                  </div>
                </div>
              </div>
              <div class="mt-10 max-w-[1000px] text-wrap">
                <div class="font-semibold text-sm text-[#FF0000]">OVERVIEW</div>
                <div class="mt-3 text-sm">{{ listMovie.overview }}</div>
              </div>
            </div>
          </div>
          <div class="mt-10 relative z-3 ml-[124px]">
            <div class="font-semibold text-sm text-[#FF0000] mb-5">REVIEWS</div>
            <div class="flex flex-row flex-wrap gap-10">
              <div v-for="review in listReview" :key="review.id" class="card-review p-5">
                <div class="flex flex-row justify-between">
                  <div class="flex flex-row gap-2">
                    <div>
                      <svg
                        xmlns="http://www.w3.org/2000/svg"
                        width="48"
                        height="48"
                        viewBox="0 0 48 48"
                        fill="none"
                      >
                        <circle
                          cx="24"
                          cy="24"
                          r="24"
                          fill="#1E232B"
                          fill-opacity="0.21"
                        />
                      </svg>
                    </div>
                    <div class="mt-1">
                      <div class="font-bold text-sm">
                        {{ review.author_details.username }}
                      </div>
                      <div class="text-xs font-normal">
                        {{ formatDate(review.updated_at) }}
                      </div>
                    </div>
                  </div>
                  <div class="review-count flex flex-row justify-center p-2">
                    <div class="align-start">
                      <img
                        src="~/assets/img/star.svg"
                        width="17"
                        height="17"
                        alt="star"
                        class="mr-2"
                      />
                    </div>

                    <div class="font-semibold text-4xl">
                      {{
                        review.author_details.rating === null
                          ? '0.0'
                          : review.author_details.rating.toFixed(1)
                      }}
                    </div>
                  </div>
                </div>
                <div class="mt-10 font-normal italic text-[13px] line-clamp-6">
                  {{ review.content }}
                </div>
              </div>
            </div>
          </div>
        </div>

        <Footer />
      </div>
    </client-only>
  </div>
</template>
<script lang="ts" setup>
// import useRouter from 'nuxt'
// const { currentRoute } = useRouter();
const route = useRoute()
const listMovie = ref(<unknown>{})
const listReview = ref([])
const getDetailMovieList = async () => {
  const { data: movie, refresh } = await useFetch(
    `https://api.themoviedb.org/3/movie/${route.params.id}?language=en-US'`,
    {
      method: 'GET',
      headers: {
        accept: 'application/json',
        Authorization:
          'Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiI0MjY3ZWE5ZjVlMDBjNTgyMzQxN2IxMDk4ZmI1YTM2OSIsInN1YiI6IjY1YWEyNGI4N2NhYTQ3MDEyYjA5NjhmOCIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.BvNPwYCOx7H87JF9NMefAG0iMpGmVpyImF_imaf5FMU',
      },
    }
  )
  listMovie.value = movie.value
  watchEffect(() => {
    refresh()
  })
}
getDetailMovieList()

const getReview = async () => {
  const { data: review, refresh } = await useFetch(
    `https://api.themoviedb.org/3/movie/${route.params.id}/reviews?language=en-US'`,
    {
      method: 'GET',
      headers: {
        accept: 'application/json',
        Authorization:
          'Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiI0MjY3ZWE5ZjVlMDBjNTgyMzQxN2IxMDk4ZmI1YTM2OSIsInN1YiI6IjY1YWEyNGI4N2NhYTQ3MDEyYjA5NjhmOCIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.BvNPwYCOx7H87JF9NMefAG0iMpGmVpyImF_imaf5FMU',
      },
    }
  )
  // console.log(review.value.results)
  listReview.value = review?.value?.results ?? {}
  watchEffect(() => {
    refresh()
  })
}

getReview()

const getYear = (data: string) => {
  console.log(data)
  // const datas = data.slice(0, 4)
  const datas = new Date(data).getFullYear()
  return datas
}

const filterGenre = (data: any) => {
  const names = data.map(function (item: any) {
    return item['name']
  })

  return names.slice(0, -1).join(', ') + ', ' + names.at(-1) + ''
}

const formatDate = (date: any) => {
  // let options =
  // console.log(date)
  return new Intl.DateTimeFormat('en-US', {
    year: 'numeric',
    month: 'long',
    day: 'numeric',
  }).format(new Date(date))
}

const formatCurrency = (digit: number) => {
  return new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD',
    maximumFractionDigits: 2,
  }).format(digit)
}
</script>
<style lang="postcss" scoped>
.page-wrapper {
  position: relative;
  min-height: 100%;
  padding-bottom: 20rem;
}

.score-bg {
  @apply relative bg-[#00000080] h-[80px] w-full;
}

.overview-bg {
  @apply relative bg-[#FFFFFF] min-h-[512px] w-full;
}

.card-review {
  width: 582px;
  height: 284px;
  border-radius: 14px;
  background: #f9f9f9;
  box-shadow: 0px 4px 4px 0px rgba(0, 0, 0, 0.1);
}
.review-count {
  width: 97px;
  height: 52px;
  border-radius: 7px;
  background: rgba(196, 196, 196, 0.28);
}
</style>
