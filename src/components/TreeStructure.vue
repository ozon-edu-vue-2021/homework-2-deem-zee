<!-- eslint-disable vue/no-use-v-if-with-v-for,vue/no-confusing-v-for-v-if -->
<template>
<div>
    <div 
         @click="clicked()"
        :style="{'margin-left': `${depth * 20}px`}"
        class="node">
        <span v-if="hasChildren && node.type == 'directory'"
        class="type"
        :style="{'cursor' : 'pointer'}">{{expanded ?  '&#128194;' : '&#128193;'}}{{node.name}}</span>
        <span v-else-if="!hasChildren  && node.type == 'file'"
        @click="select()"
        :class="{'active-node': selected}"
        >{{'&#128196;'}}{{node.name}}</span>
        <span v-else
        @click="select()"
        :class="{'active-node': selected}">{{'&#128279;'}}{{node.name}}</span>
    </div>
    <div  v-if="expanded">
      <TreeStructure 
        v-for="child in node.contents"
        :key="child.name"
        :node="child"
        :depth="depth + 1" 
    />  
    </div>
    
</div>
</template>

<script>

export default ({
    name: 'TreeStructure',
    props: {
        node: Object,
        depth: {
            type: Number,
            default: 0,
        },
    
    },
    data() {
        return {
            expanded: false,
            selected: false,
            selectedNode: null,
        }
    }, 
    methods: {
        clicked() {
            this.expanded = !this.expanded;
        },
        select() {
           let active = document.querySelector('.active-node')
           if(active === null) {
               this.selected = true;
           } else {
               active.classList.remove('active-node');
               this.selected = true;
           }
        },
        
    },
    computed: {
        hasChildren () {
            return this.node.contents;
        },
    }
})
</script>

<style scoped>
    .node {
        text-align: left;
        font-size: 24px;
    }
    .active-node {
        background: blue;
    }
</style>