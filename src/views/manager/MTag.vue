<template>
  <div>
    <div
      class="tag"
    >
      <a
        class="p"
        v-for="(t, index) in tags"
        :key="index"
        :style="t.style"
        :href="'/manager/tag/'+t.id+'?tname='+t.name"
      >
        #{{ t.name }}
      </a>
    </div>
  </div>
</template>

<script>
    import {getTagList} from '@/api/app'

    export default {
        name: "MTag",
        data() {
            return {
                tags: []
            }
        },
        methods: {
            getData() {
                getTagList().then(res => {
                    console.log(res)
                    if (res.code === 200) {
                        this.tags = res.list;
                    }
                }).catch(res => {
                    this.$message.error('请求失败');
                    console.log("请求失败");
                    console.log(res);
                });

            },
        },
        mounted() {
            this.getData();
        }
    }
</script>

<style scoped>
    .tag {
        width: 50%;
        margin-left: 17%;
        margin-top: 5%;
        height: 60%;
    }
    .p {
        margin-left: 33px;
        margin-top: 22px;
        display:inline-block;
    }
</style>