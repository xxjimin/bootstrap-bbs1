<template>
    <div>
        <b-table striped hover :items="items" :fields="fields" 
        :per-page="perPage"
        :current-page="currentPage"
        @row-clicked="rowClick"></b-table>
        <b-pagination
        align="center"
        v-model="currentPage"
        :total-rows="rows"
        :per-page="perPage"></b-pagination>
        <b-button @click="writeContent">글쓰기</b-button>
    </div>
</template>
<script>
import data from '@/components/data/index'


export default {
    data() {
        let items = data.Content.sort((a,b) => {return b.content_id-a.content_id})
        items = items.map(contentItem => {return{...contentItem, user_name: data.User.filter(userItem => userItem.user_id === contentItem.user_id)[0].name}})
        return{
            currentPage:1,
            perPage: 10,
            fields: [
                {
                    key: 'content_id',
                    label: '글번호'
                },
                {
                    key: 'title',
                    label: '글제목'
                },
                {
                    key: 'created_at',
                    label: '게시 시간'
                },
                {
                    key: 'user_name',
                    label: '글쓴이'
                },
            ],
            items: items
        }
    },
    methods: {
        rowClick(item, index, e){
            this.$router.push({
                path: `/board/free/detail/${item.content_id}`
            })
        },

        writeContent(){
            this.$router.push({
                path: '/board/free/create'
            })
        }
    },

    computed:{
        rows(){
            return this.items.length
        }
    }
};
</script>