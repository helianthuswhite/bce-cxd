<template>
    <div class="file-list">
        <Search @search="search" />
        <div class="main-container">
            <Folder v-for="folder in folderList" @refresh="refresh" :name="folder.key" :back="folder.back" @back="back" />
            <File v-for="file in fileList" :src="file.src" :name="file.key" />
        </div>
    </div>
</template>

<script>
import api from '../api/api';
import {CDNHost, BucketName} from '../config/config';

import Search from './Search';
import File from './File';
import Folder from './Folder';

export default {
    name: 'FileList',
    components: {
        Search,
        Folder,
        File
    },
    data() {
        return {
            fileList: [],
            folderList: [],
            prefix: '',
            afterSearch: false
        }
    },
    created() {
        this.initData();
    },
    methods: {
        refresh(e) {
            this.prefix += e;
            this.initData();
        },
        search(keyword) {
            this.prefix = keyword;
            this.afterSearch = true;
            this.initData();
        },
        back() {
            const prefixArr = this.prefix.split('/');
            prefixArr.splice(-2, 1);
            this.prefix = prefixArr.join('/');

            this.initData();
        },
        initData() {
            const bucketName = BucketName;
            const options = {
                delimiter: '/',
                prefix: this.prefix
            };            

            api.listObjects(bucketName, options).then(data => {
                const {folders, objects, prefix} = data;

                console.log(data);

                objects.forEach(object => {
                    object.src = CDNHost + object.key;
                });

                if (prefix) {

                    if (!this.afterSearch) {
                        objects.forEach(object => {
                            object.key = object.key.substring(prefix.length);
                        });

                        folders.forEach(folder => {
                            folder.key = folder.key.substring(prefix.length);
                        });
                    }

                    const obj = {
                        key: '返回上级',
                        back: true
                    };
                    folders.unshift(obj);
                }

                this.fileList = objects;
                this.folderList = folders;
                this.prefix = prefix;
            });
        }
    }
};
</script>

<style>
    .main-container {
        display: flex;
        flex-wrap: wrap;
        max-width: 1200px;
    }
</style>
