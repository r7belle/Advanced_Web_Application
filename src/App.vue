<template>
  <div id="app">
    <BaseCondition/>
    <BaseLoop />
    <FlexBox :showComponents="true"/>
  </div>
</template>

<script>
import BaseCondition from './Components/BaseCondition.vue';
import BaseLoop from './Components/BaseLoop.vue';
import FlexBox from './Components/FlexBox.vue';
export default {
  components: {
    BaseCondition,
    BaseLoop,
    FlexBox,
  },
};
</script>

<style>
body {
  margin: 0;
  font-family: 'Helvetica Neue', sans-serif;
}
</style>