<template>
  <div class="hello">
    <Counter
      :year="2021"
      :month="2"
      :date="25"
      :hour="5"
      :minute="59"
      :second="59"
      :millisecond="59"
    />
  </div>
</template>

<script>
import Counter from "../components/Counter";
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  components: {
    Counter,
  },
};
</script>
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
