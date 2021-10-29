<template>
    <div
        v-on="$listeners"
        class="link-wrapper"
    >
        <img class="link-img" src="../assets/images/link.png" alt="Link">
        <p>
            {{ name }}
        </p>
    </div>
</template>

<script>

export default {
    name: 'Link',

    props: {
        name: {
            tepy: String,
            default: '',
        }
    }
}
</script>

<style scoped>
.link-wrapper {
    display: flex;
    align-items: center;
    text-decoration: underline;
    color: blue;
    cursor: pointer;
}
.link-img {
    width: 40px;
    height: auto;
    margin: 0 8px 0 0;
}
</style>
