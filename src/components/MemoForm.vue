<template>
  <div>
    <p>タイトル</p>
    <input type="text" v-model="title"/>
  </div>
  <div>
    <p>本文</p>
    <textarea v-model="content"></textarea></div>
  <div class="ceater">
    <button @click="save">保存</button>
    <button @click="remove" v-if="memo.id">削除</button>
    </div>
</template>

<script>
export default {
  name: 'MemoForm',
  props:[
    'memo'
  ],
  data(){
    return{
      title:this.memo.title,
      content:this.memo.content
    }
  },
  methods:{
    save(){
      let memo ={
        title:this.title,
        content:this.content
      }
      if(this.memo.id){
        memo.id=this.memo.id
      }
      this.$store.commit('save',memo)
      this.$router.push('/')
    },
    remove(){
      this.$store.commit('delete',this.memo.id)
      this.$router.push('/')
    }
  }
}
</script>

<style scoped>
  p{
    text-align: left;

  }

  div{
    margin-bottom: 10px;
  }
  input[type=text] {
    width: 100%;
    height: 25px;

  }
  textarea{
    width: 100%;
    height: 30rem;

  }
  .center{
    text-align: center;
  }
</style>