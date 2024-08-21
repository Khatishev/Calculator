<template>
  <button class="cell" :class="{ 'num': type === 'num', 'delete': type === 'delete' }" @click="handleClick">{{ label }}</button>
</template>

<script>
export default {
  props: ['label', 'type', 'handleClick'],
}
</script>

<style scoped></style>