<template>
  <div class="add-timer">
    <div class="add-timer__plus-v" />
    <div class="add-timer__plus-h" />
  </div>
</template>

<script>
export default {
  name: "PlusTimer",
};
</script>

<style>
.add-timer {
  width: 100%;
  height: 100%;
  background-color: #696969;
  position: relative;
  transition: all 0.3s ease-in-out;
}

.add-timer:hover {
  cursor: pointer;
  box-shadow: 0px 5px 10px 2px rgba(158, 158, 158, 0.2);
  transition: all 0.3s ease-in-out;
}

.add-timer__plus-v {
  width: 3px;
  height: 20px;
  background-color: #9e9e9e;
  position: absolute;
  top: 50px;
  left: 111px;
}

.add-timer__plus-h {
  width: 20px;
  height: 3px;
  background-color: #9e9e9e;
  position: absolute;
  top: 58.5px;
  left: 102.5px;
}
</style>