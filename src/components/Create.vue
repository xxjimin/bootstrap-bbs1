<template>
    <div>
        <b-input v-model="subject" placeholder="제목을 입력하여 주십시오"></b-input>
        <b-form-textarea
            v-model="context"
            placeholder="내용을 입력해 주세요"
            rows="3"
            max-rows="6">
        </b-form-textarea>
        <b-button @click="uploadContent">저장</b-button>
        <b-button @click="cancel">취소</b-button>
    </div>
</template>
<script>
import data from '@/components/data'
export default {
    name: 'Create',
    data(){
        return {
            subject: '',
            context: '',
            user_id: 1,
            created_at: '2024-02-19 14:43:32',
            updated_at: null
        }
    },
    
    methods: {
        cancel(){
            this.$router.push({
                path: '/board/free/'
            })
        },

        uploadContent(){

            let items = data.Content.sort((a,b) => {return b.content_id - a.content_id})
            const content_id = items[0].content_id + 1
            data.Content.push({
                content_id: content_id,
                user_id: this.user_id,
                title: this.subject,
                context: this.context,
                created_at: this.created_at,
                updated_at: this.updated_at
            })

            this.$router.push({
                path: '/board/free/'
            })

        }
    },
}
</script>