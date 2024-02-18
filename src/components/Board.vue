<template>
    <div>
        <b-table striped hover :items="items" :fields="fields"></b-table>
    </div>
</template>
<script>
import data from '@/components/data/index'
let items = data.Content.sort((a,b) => {return b.content_id-a.content_id})
items = items.map(contentItem => {return{...contentItem, user_name: data.User.filter(userItem => userItem.user_id === contentItem.user_id)[0].name}})
export default {
    data() {
        return{
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
        };
    }
};
</script>