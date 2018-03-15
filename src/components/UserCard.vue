<template>
  <div class="Card">
    <div class="Card-top">
      <img class="Card-top__img" :src="user.photo" :alt="user.fullName">
    </div>
    <div class="Card-middle">
      <p class="Card-middle__title" v-text="userTitle"></p>
      <h2 v-if="userValue.name" class="Card-middle__value" v-text="user.fullName"></h2>
      <h2 v-if="userValue.brithday" class="Card-middle__value" v-text="user.birthday"></h2>
      <h2 v-if="userValue.address" class="Card-middle__value" v-text="user.address"></h2>
      <h2 v-if="userValue.phone" class="Card-middle__value" v-text="user.phone"></h2>
    </div>
    <div @mouseover="test($event)" class="Card-bottom">
      <i class="Card-bottom__icon fas fa-user fa-2x"></i>
      <i class="Card-bottom__icon fas fa-calendar-alt fa-2x"></i>
      <i class="Card-bottom__icon fas fa-location-arrow fa-2x"></i>
      <i class="Card-bottom__icon fas fa-phone fa-2x"></i>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    user: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      userTitle: "Hi, My name is",
      userValue: {
        name: true,
        brithday: false,
        address: false,
        phone: false
      }
    };
  },
  methods: {
    test(e) {
      if (e.target.classList.contains("Card-bottom__icon")) {
        if (e.target.classList.contains("fa-user")) {
          (this.userTitle = "Hi, My name is"),
            (this.userValue.name = true),
            (this.userValue.brithday = false),
            (this.userValue.address = false),
            (this.userValue.phone = false);
        } else if (e.target.classList.contains("fa-calendar-alt")) {
          (this.userTitle = "My brithday is"),
            (this.userValue.name = false),
            (this.userValue.brithday = true),
            (this.userValue.address = false),
            (this.userValue.phone = false);
        } else if (e.target.classList.contains("fa-location-arrow")) {
          (this.userTitle = "My address is"),
            (this.userValue.name = false),
            (this.userValue.brithday = false),
            (this.userValue.address = true),
            (this.userValue.phone = false);
        } else {
          (this.userTitle = "My phone number is"),
            (this.userValue.name = false),
            (this.userValue.brithday = false),
            (this.userValue.address = false),
            (this.userValue.phone = true);
        }
      }
    }
  }
};
</script>

<style lang="scss">
@import "../scss/styles.scss";

.Card {
  position: relative;
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: auto 1fr 0.75fr;
  width: 320px;
  height: 370px;
  padding: 1em 0;
  background-color: #fff;
  border-radius: 0 0 10px 10px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
  transition: all 0.3s cubic-bezier(0.25, 0.8, 0.25, 1);

  &::before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100px;
    @include var(background-color, secondary);
    border-bottom: 1px solid #ddd;
    border-radius: 10px 10px 0 0;
  }

  &:hover {
    box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25), 0 10px 10px rgba(0, 0, 0, 0.22);
  }

  &-top {
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 145px;
    height: 145px;
    margin: 0 auto;
    border-radius: 50%;
    border: 1px solid #ddd;
    background-color: #fff;

    &__img {
      border-radius: 50%;
    }
  }

  &-middle {
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    align-items: center;
    // background-color: salmon;

    &__title {
      color: rgba(map-get($vars, primary), 0.5);
      font-size: 1.15rem;
      padding: 0.25rem 0;
    }

    &__value {
      font-size: 2rem;
      text-transform: capitalize;
    }
  }

  &-bottom {
    display: flex;
    justify-content: center;
    align-items: flex-end;
    // background-color: lightgreen;

    &__icon {
      margin: 0 1rem;
      cursor: pointer;
      transition: all 0.3s cubic-bezier(0.25, 0.8, 0.25, 1);

      &:hover {
        // @include var(color, accent);
        color: rgba(map-get($vars, accent), 0.75);
      }
    }
  }
}
</style>