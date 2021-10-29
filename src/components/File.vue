<template>
    <div 
    class="file-wrapper"
    v-on="$listeners"
    >
        <img class="file-img" src="../assets/images/file.png" alt="File">
        <p>{{ name }}</p>
    </div>
</template>

<script>

export default {
    name: 'File',

    props: {
        name: {
            type: String,
            default: '',
        }
    }
}
</script>

<style scoped>
.file-wrapper {
    display: flex;
    cursor: pointer;
}
.file-img {
    width: 40px;
    height: 40px;
    margin: 0 8px 0 0;
}
</style>