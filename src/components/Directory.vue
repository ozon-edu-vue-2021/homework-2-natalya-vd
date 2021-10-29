
<template>
    <div>
        <div 
            class="directory-wrapper" 
            v-if="items.type === 'directory'"
        >
            <div class="directory-inner">
                <img class="directory-img" src="../assets/images/directory.png" alt="Directory">
                <p>{{ items.name }}</p>
            </div>
            <button 
                @click="open"
                v-show="items.contents.length"
                class="button-open"
            >
                <icon-drop-down 
                :is-open="[isOpen, isShow]"
            />
            </button>
        </div>

        <div 
            v-if="isOpen" 
            v-show="isShow"  
            class="directory-open"
        >
            <directory
                v-for="(tree, i) in items.contents"
                :key="`${tree.name}-${i}`"
                :items="tree"
                @emitPath="chengedPath($event)"
            />
        </div>

        <file 
            v-if="items.type === 'file'"
            @click="selectHandler(items)"
            @keyup.enter="selectHandler(items)"
            :class="[{'active': selectedMap[items.name]}]"
            :name="`${items.name}`"
            tabindex="0"
        />
        <Link 
            v-if="items.type === 'link'"
            @click="selectHandler(items)"
            @keyup.enter="selectHandler(items)"
            :class="[{'active': selectedMap[items.name]}]"
            :name="`${items.name}`"
            tabindex="0"
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
        isShow: true,
        selectedMap: {}
    }),

    props: {
        items: {
            type: Object,
            default: () => ({})
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

            this.$emit('emitPath', {name: items.name, isShow: this.isShow})
        },

        open() {
            if(this.isOpen) {
                this.isShow = !this.isShow;
            } else {
                this.isOpen = true;
            }

            this.$emit('emitPath', {name: this.items.name, isShow: this.isShow});
        },

        chengedPath(event) {
            this.$emit('emitPath', {name: `${this.items.name}/${event.name}`, isShow: event.isShow})
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

.button-open {
    cursor: pointer;
}

.active {
    background-color: lightcyan;
}
</style>