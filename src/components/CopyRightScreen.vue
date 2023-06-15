<template>
  <div class="copyright">
    <p>This game owned by TAN in Vue 3 <a>Or</a></p>
  </div>
</template>

<script>
export default {};
</script>

<style>
.copyright {
  position: fixed;
  left: 50%;
  transform: translateX(-50%);
  bottom: 1.5rem;
  color: var(--light);
  z-index: 3;
  font-size: 1.5rem;
}

.copyright a {
  color: #f4dc26;
}
</style>
