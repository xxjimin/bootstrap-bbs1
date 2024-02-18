<template>
    <div>
        <b-table striped hover :items="items" :fields="fields"></b-table>
    </div>
</template>
<script>
import data from '@/components/data/index'
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
            ],
            items: data.Content
        };
    }
};
</script>