<template>
    <div>
        <div :key="item.comment_id" v-for = "item in comments">
            <CommentListItem :commentObj="item"/></div>
            <CommentCreate :contentId="contentId" :reloadComments="reloadComments"/>
    </div>
</template>
<script>
import data from '@/components/data';
import CommentListItem from '@/components/CommentListItem';
import CommentCreate from '@/components/CommentCreate.vue';


export default {
    name: 'CommentList',
    components: { 
        CommentListItem,
        CommentCreate
     },
    
    props: {
        contentId: Number,
    },

    data() {
        return {
            comments: data.Comment.filter(item => item.content_id === this.contentId)
        };
    },

    methods:{
        reloadComments(){
            this.comments = data.Comment.filter(item => item.content_id === this.contentId)
        }
    }
    
}
</script>