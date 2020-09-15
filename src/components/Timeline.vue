<template>
  <ul>
    <li class="date" :data-date="formattedDates">
      <h1>{{ fullName }}</h1>
      <p class="tags">tags: {{ tags }}</p>
      <p>{{ item.about }}</p>
    </li>
  </ul>
</template>

<script>
import moment from "moment";

export default {
  name: "Timeline",
  props: ["item"],
  computed: {
    fullName() {
      return `${this.item.name.first} ${this.item.name.last}`;
    },
    tags() {
      return this.item.tags.toString();
    },
    formattedDates() {
      let dates = new Date(this.item.registered);
      return moment(dates).format("LL");
    },
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css?family=Chivo:300,300i,400,400i,600|Saira:400");

$background: #fafafa;
$color-primary: #0b5184;
$font-title: "Saira", sans-serif;
$font-text: "Chivo", sans-serif;

body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  background: $background;
  font-size: 1rem;
  font-weight: 300;
}

.tags {
  font-style: italic;
  font-weight: 400;
  color: rgba(0, 0, 0, 0.6);
}

ul {
  border-left: 4px solid $color-primary;
  font-family: $font-text;
  margin: 0 auto;
  letter-spacing: 0.5px;
  position: relative;
  line-height: 1.4em;
  font-size: 1rem;
  padding: 50px;
  list-style: none;
  text-align: left;
  font-weight: 100;
  max-width: 30%;

  h1 {
    font-family: $font-title;
    letter-spacing: 1.5px;
    font-weight: 400;
    font-size: 1.4em;
  }

  .date {
    position: relative;

    &:before,
    &:after {
      position: absolute;
    }

    &:before {
      left: -14rem;
      content: attr(data-date);
      text-align: right;
      font-weight: 500;
      font-size: 0.9em;
      min-width: 120px;
      font-family: $font-title;
    }

    &:after {
      left: -4.1rem;
      background: $color-primary;
      border: solid 4px lighten($color-primary, 60%);
      border-radius: 50%;
      height: 1.2rem;
      width: 1.2rem;
      content: "";
      top: 0;
    }
  }
}
</style>
