
<template>
    <div>
        <div 
            v-if="items.type === 'directory'"
        >
            <div class="directory-wrapper">
                <div class="directory-inner">
                    <img class="directory-img" src="../assets/images/directory.png" alt="Directory">
                    <p>{{ items.name }}</p>
                    
                </div>
                <icon-drop-down 
                    @click="open"
                    v-show="items.contents.length"
                    :is-open="isOpen"
                />
            </div>

            <div v-if="isOpen" class="directory-open">
                <directory
                    v-for="(tree, i) in items.contents"
                    :key="`${tree.name}-${i}`"
                    :items="tree"
                    :prop-path="propPath"
                />
            </div>
        </div>

        <file 
            v-if="items.type === 'file'"
            @click="selectHandler(items)"
            :class="[{'active': selectedMap[items.name]}]"
            :name="`${items.name}`"
        />
        <Link 
            v-if="items.type === 'link'"
            @click="selectHandler(items)"
            :class="[{'active': selectedMap[items.name]}]"
            :name="`${items.name}`"
            :target="`${items.target}`"
        />
    </div>
</template>



<script>
import IconDropDown from './Icons/IconDropDown.vue';
import File from './File.vue';
import Link from './Link.vue';
import Vue from "vue";

export default {
    name: 'Directory',

    data: () => ({
        isOpen: false,
        selectedMap: {},
    }),

    props: {
        items: {
            type: Object,
            default: () => ({})
        },

        propPath: {
            type: String,
            default: 'path-default'
        }
    },

    components: {
        File,
        Link,
        IconDropDown
    },

    methods: {
        selectHandler(items) {
            this.selectedMap[items.name]
            ? Vue.delete(this.selectedMap, items.name)
            : Vue.set(this.selectedMap, items.name, items);

            this.$parent.$emit('emitPath', `${this.propPath}/${items.name}`)
        },

        open() {
            return this.isOpen = !this.isOpen;
        }
    },
}
</script>

<style scoped>
.directory-open {
    margin: 0 0 0 20px;
}

.directory-wrapper {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.directory-inner {
    display: flex;
}

.directory-img {
    width: 40px;
    height: auto;
    margin: 0 8px 0 0;
}

.active {
    background-color: lightcyan;
}
</style>