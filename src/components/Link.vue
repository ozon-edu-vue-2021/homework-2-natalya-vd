<template>
    <div
        v-on="$listeners"
    >
        <a class="link" :href="target"><img class="link-img" src="../assets/images/link.png" alt="Link">{{ name }}</a>
    </div>
</template>

<script>

export default {
    name: 'Link',

    props: {
        name: {
            tepy: String,
            default: '',
        },

        target: {
            type: String,
            default: 'link'
        }
    }
}
</script>

<style scoped>
.link {
    display: flex;
    align-items: center;
}
.link-img {
    width: 40px;
    height: auto;
    margin: 0 8px 0 0;
}
</style>
