<template>
    <div class="file" @click="onClick">
        <img :src="src" width="100">
        <h2 class="name">{{name}}</h2>
    </div>
</template>

<script>

export default {
    name: 'Folder',
    props: {
        src: {
            default: 'http://baiduyun-icon.cdn.bcebos.com/images/nofile.svg',
        },
        name: {
            default: 'default'
        },
        back: {
            default: false
        }
    },
    methods: {
        onClick() {
            this.back ? this.$emit('back') : this.$emit('refresh', this.name);
        }
    }
};
</script>

<style lang="less">
</style>
