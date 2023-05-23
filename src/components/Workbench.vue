<template>
  <div class="container">
    <div class="outer1">
      <div class="inner1">css</div>
    </div>
    <div class="outer2">
      <div class="inner2">flexbox</div>
    </div>
  </div>
</template>

<script>
</script>

<style scoped lang="scss">
@import "../style.scss";

.container {
  display: flex;
  margin-top: 20px;
}
.outer1,
.outer2 {
  border: 5px solid $primary-color;
  height: 500px;
  width: 500px;

}
.inner1,
.inner2 {
  width: 100px;
  height: 100px;
  background-color: $primary-color;
}

.outer1 {
  position: relative;
}
.inner1 {
  position: absolute;
  margin: 0;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.outer2 {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>