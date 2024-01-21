<template>
  <nav
    class="flex-no-wrap fixed top-0 z-10 flex w-full items-center justify-between bg-[#FFFFFF0D] py-2 shadow-md shadow-black/5 lg:flex-wrap lg:justify-start lg:py-4 h-[66px]"
  >
    <div class="flex w-full flex-wrap items-center justify-around px-3">
      <!-- <div class="flex-grow basis-[100%] items-center lg:!flex lg:basis-auto"> -->
      <!-- Logo -->
      <div class="flex ml-14">
        <NuxtLink
          class="mb-4 ml-2 mr-5 mt-3 flex items-center text-neutral-900 lg:mb-0 lg:mt-0"
          to="/"
        >
          <img
            src="~/assets/img/logo-color.png"
            height="31"
            width="112"
            alt="Moovie Time Logo"
            loading="lazy"
          />
        </NuxtLink>
        <div>
          <form class="w-[576px] h-[36px]">
            <div class="relative">
              <div
                class="absolute inset-y-0 start-0 flex items-center ps-3 pointer-events-none"
              >
                <!-- <svg
                class="w-4 h-4 text-gray-500 dark:text-gray-400"
                aria-hidden="true"
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 20 20"
              >
                <path
                  stroke="currentColor"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="m19 19-4-4m0-7A7 7 0 1 1 1 8a7 7 0 0 1 14 0Z"
                />
              </svg> -->
                <img src="~/assets/icon/icon-find-movie.svg" alt="icon movie" />
              </div>
              <input
                type="input"
                class="block w-full p-[0.4rem] ps-10 text-base text-[#E5E5E5] bg-[#00000021]"
                placeholder="Find movie"
              />
              <svg
                class="w-4 h-4 absolute end-2.5 bottom-2.5 text-gray-500 dark:text-gray-400"
                aria-hidden="true"
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 20 20"
              >
                <path
                  stroke="currentColor"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="m19 19-4-4m0-7A7 7 0 1 1 1 8a7 7 0 0 1 14 0Z"
                />
              </svg>
              <!-- <button
              type="submit"
              class="text-white absolute end-2.5 bottom-2.5 bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-4 py-2 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
            >
              Search
            </button> -->
            </div>
          </form>
        </div>
      </div>

      <!-- Left navigation links -->
      <ul class="list-style-none flex justify-between mr-7">
        <li class="mb-4 lg:mb-0 lg:pr-2">
          <!-- Projects link -->
          <a
            class="text-neutral-500 flex transition duration-200 hover:text-neutral-700 hover:ease-in-out focus:text-neutral-700 disabled:text-black/30 motion-reduce:transition-none dark:text-neutral-200 dark:hover:text-neutral-300 dark:focus:text-neutral-300 lg:px-6 [&.active]:text-black/90 dark:[&.active]:text-zinc-400"
            href="#"
          >
            <img src="~/assets/icon/icon-grid.svg" alt="icon grid" class="mr-2" />
            Categories
          </a>
        </li>
        <!-- About me link -->
        <li class="mb-4 lg:mb-0 lg:pr-2">
          <a
            class="text-neutral-500 transition duration-200 hover:text-neutral-700 hover:ease-in-out focus:text-neutral-700 disabled:text-black/30 motion-reduce:transition-none dark:text-neutral-200 dark:hover:text-neutral-300 dark:focus:text-neutral-300 lg:px-6 [&.active]:text-black/90 dark:[&.active]:text-neutral-400"
            href="#"
            >Movies</a
          >
        </li>
        <!-- Testimonials link -->
        <li class="mb-4 lg:mb-0 lg:pr-2">
          <a
            class="text-neutral-500 transition duration-200 hover:text-neutral-700 hover:ease-in-out focus:text-neutral-700 disabled:text-black/30 motion-reduce:transition-none dark:text-neutral-200 dark:hover:text-neutral-300 dark:focus:text-neutral-300 lg:px-6 [&.active]:text-black/90 dark:[&.active]:text-neutral-400"
            href="#"
            >TV Show</a
          >
        </li>
        <!-- Contact link -->
        <li class="mb-4 lg:mb-0 lg:pr-2">
          <a
            class="text-neutral-500 transition duration-200 hover:text-neutral-700 hover:ease-in-out focus:text-neutral-700 disabled:text-black/30 motion-reduce:transition-none dark:text-neutral-200 dark:hover:text-neutral-300 dark:focus:text-neutral-300 lg:px-6 [&.active]:text-black/90 dark:[&.active]:text-neutral-400"
            href="#"
            >Login</a
          >
        </li>
      </ul>
      <!-- </div> -->
    </div>
  </nav>
  <!-- Navbar -->
</template>
