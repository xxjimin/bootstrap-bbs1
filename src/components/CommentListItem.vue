<template>
    <div>
        <div class="comment-list-item">

      <div class="comment-list-item-name">
        <div>{{ name }}</div>
        <div>{{ commentObj.created_at }}</div>
      </div>

      <div class="comment-list-item-context">{{ commentObj.context }}</div>

      <div class="comment-list-item-button">
        <b-button variant="info">수정</b-button>
        <b-button variant="info">삭제</b-button>
        <b-button variant="info" @click="changesubCommentCreateToggle">답글 달기</b-button>
      </div>
    </div>
    <template v-if="subCommentCreateToggle">
        <div>
            <CommentCreate 
            :isSubComment="true" 
            :commentId="commentObj.comment_id"
            :reloadSubComments="reloadSubComments"
            :changesubCommentCreateToggle="changesubCommentCreateToggle"/>
        </div>
        
    </template>
    <template v-if="subCommentList.length > 0">
      <div
        class="comment-list-item-Subcomment-list"
        :key="item.subcomment_id"
        v-for="item in subCommentList"
      >
        <div class="comment-list-item-name">
          <div>{{item.user_name}}</div>
          <div>{{item.created_at}}</div>
        </div>
        <div class="comment-list-item-context">{{item.context}}</div>
        <div class="comment-list-item-button">
          <b-button variant="info">수정</b-button>
          <b-button variant="info">삭제</b-button>
        </div>
      </div>
    </template>

    </div>
</template>
<script>
import data from '@/components/data'
import CommentCreate from '@/components/CommentCreate'
export default {
  components: { CommentCreate },
    name: 'CommentListItem',
    props:{
        commentObj: Object,

    },
    data(){
        return{
            name: data.User.filter(
                item => item.user_id === this.commentObj.user_id
            )[0].name,

            subCommentList: data.SubComment.filter(
                item => item.comment_id === this.commentObj.comment_id
            ).map(subCommentItem => ({
                ...subCommentItem,
                user_name: data.User.filter(
                item => item.user_id === this.commentObj.user_id
            )[0].name
            })),
            subCommentCreateToggle: false,
        };
    },

    methods:{
        changesubCommentCreateToggle(){
            this.subCommentCreateToggle = !this.subCommentCreateToggle;
        },

        reloadSubComments() {
      this.subCommentList = data.SubComment.filter(
        item => item.comment_id === this.commentObj.comment_id
      ).map(subCommentItem => ({
        ...subCommentItem,
        user_name: data.User.filter(
          item => item.user_id === subCommentItem.user_id
        )[0].name 
      }));
    }}
};
</script> 
<style scoped>
.comment-list-item {
  display: flex;
  justify-content: space-between;
  padding-bottom: 1em;
}

.comment-list-item-name {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  border: 0.5px solid black;
  padding: 1em;
}

.comment-list-item-context {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 50em;
  border: 0.5px solid black;
}

.comment-list-item-button {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  border: 0.5px solid black;
  padding: 1em;
}

.btn {
  margin-bottom: 1em;
}

.comment-list-item-Subcomment-list {
  display: flex;
  justify-content: space-between;
  padding-bottom: 1em;
  margin-left: 10em;
}
</style>