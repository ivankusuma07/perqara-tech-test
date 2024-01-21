<template>
  <footer class="footer">
    <div class="wrapper-footer">
      <div class="ml-[64px]">© 2021 MoovieTime. All rights reserved.</div>
      <div class="-ml-[8.5rem]"><img src="~/assets/img/logo-grey.svg" alt="logo" /></div>
      <div class="mr-[64px]">
        Made with <a href="https://nuxt.com/" class="underline">Nuxt 3</a>
      </div>
    </div>
  </footer>
</template>
<style lang="postcss">
.wrapper-footer {
  @apply flex justify-between p-14 bg-[#0000004A] text-[#929292] h-[160px] align-middle text-[13px] font-normal;
}
.footer {
  position: absolute;
  bottom: 0;
  width: 100%;
}
</style>
