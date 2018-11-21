<template>
    <div class="search-box">
        <div class="button" @click="onClick">搜索</div>
        <input v-model="keyword" type="text" />
    </div>
</template>

<script>

export default {
    name: 'FileList',
    data() {
        return {
            keyword: 'asdad'
        };
    },
    methods: {
        onClick() {
            this.$emit('search', this.keyword);
        }
    }
};
</script>

<style <style lang="less">
    .search-box {
        width: 100%;

        &::after {
            content: '';
            display: block;
            clear: both;
        }

        > * {
            float: right;
        }
        
        input {
            height: 30px;
        }

        .button {
            width: 100px;
            line-height: 30px;
            text-align: center;
            display: inline-block;
            background: #108cee;
            color: #fff;
            margin-left: 20px;
            cursor: pointer;
        }
    }
</style>
