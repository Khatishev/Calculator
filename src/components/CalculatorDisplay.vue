<template>
    <input class="inp" :value="value" placeholder="0" readonly />
</template>

<script>
export default {
    props: ['value']
}
</script>
<style scoped></style>