<template>
  <header class="Header">
    <h1 class="Header__title">{{ title }}</h1>
    <h2 class="Header__subtitle">{{ subtitle }}</h2>
  </header>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      required: true
    },
    subtitle: {
      type: String,
      required: true
    }
  }
};
</script>

<style lang="scss">
@import "../scss/styles.scss";

.Header {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  @include var(background-color, primary);
  @include var(color, secondary);

  &__title,
  &__subtitle {
    @include fontWeight(light);
    padding: 0.25rem 0;
  }

  &__title {
    font-size: 2.25rem;

    @include from(m) {
      font-size: 3rem;
    }

    @include from(l) {
      font-size: 4rem;
    }
  }

  &__subtitle {
    @include from(l) {
      font-size: 1.75rem;
    }
  }
}
</style>
