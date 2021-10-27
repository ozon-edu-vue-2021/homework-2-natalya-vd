<template>
    <div 
        class="list-wrapper"
    >
        <h2>
            Путь: {{ path }}
        </h2>
        <directory
            :items="items"
            :prop-path="this.items.name"
            @emitPath="chengedPath($event)"
        />
    </div>
</template>

<script>

import Directory from './Directory.vue';

export default {
    name: 'List',

    data() {
        return {
            path: 'component'
            }
    },

    props: {
        items: {
            type: Object,
            default: () => ({})
        }
    },

    components: {
        Directory
    },

    created() {
        this.path = this.items.name;
    },

    methods: {
        chengedPath(event) {
            if(!this.path.includes(event)) {
                this.path = event
            }
        }
    }
}
</script>

<style scoped>
.list-wrapper {
    width: 600px;
    margin: 0 auto;
    font-size: 18px;
}
</style>