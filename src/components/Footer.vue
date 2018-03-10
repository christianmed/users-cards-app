<template>
  <footer class="Footer">
    <p class="Footer__copyright">
      {{ copyright }}
    </p>
  </footer>
</template>

<script>
export default {
  props: {
    copyright: {
      type: String,
      required: true
    }
  }
};
</script>

<style lang="scss">
@import "../scss/styles.scss";

.Footer {
  @include var(background-color, accent);

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  @include var(background-color, primary);
  @include var(color, secondary);
}
</style>
