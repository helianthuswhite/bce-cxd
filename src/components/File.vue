<template>
    <div>
        <div class="file" v-clipboard:copy="src" v-clipboard:success="onCopy">
            <img :src="src" width="100">
            <h2 class="name">{{name}}</h2>
        </div>
    </div>
</template>

<script>

export default {
    name: 'File',
    props: {
        src: {
            default: 'http://baiduyun-icon.cdn.bcebos.com/images/nofile.svg',
        },
        name: {
            default: 'default'
        }
    },
    methods: {
        onCopy() {
            alert('复制文件链接成功！');
        }
    }
};
</script>

<style lang="less">
    .file {
        text-align: center;
        height: 120px;
        // border: solid 1px #ebebeb;
        margin: 20px 10px;
        cursor: pointer;

        img {
            line-height: 100px;
            height: 100px;
        }

        h2 {
            font-size: 12px;
            text-align: center;
        }
    }
</style>
