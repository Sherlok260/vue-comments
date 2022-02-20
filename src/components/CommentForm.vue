<template>
    <div>
        <h3>Add Commet</h3>
            <form @submit.prevent>
              <input class="form-line" v-model="comment.name" type="text" placeholder="Name...">
              <input class="form-line"  v-model="comment.email" type="email" placeholder="Email...">
              <input class="form-line"  v-model="comment.body" type="email" placeholder="Body...">
              <button class="bttn" @click="add">Add comment</button>
            </form>
    </div>
</template>

<script>
export default {
    data(){
        return {
            comment: {
                name: "",
                email: "",
                body: ""
            }
        }
    },
    methods: {
        add(){
            const newcomment = {
                id: new Date(),
                name: this.comment.name,
                email: this.comment.email,
                body: this.comment.body
            }
            // this.comments.push(newcomment);
            this.$emit('createComment', newcomment)

            this.comment = {
                name: "",
                email: "",
                body: ""
            }
        }
    },
    watch: {
    comment: {
      handler(newValue) {
        console.log(newValue);
      }, deep: true
    }
  }
}
</script>

<style scoped>
    .form-line {
        border: none;
        margin-top: 10px;
        margin-bottom: 10px;
        padding: 10px;
        border-radius: 4px;
        display: inline-block;
        box-sizing: border-box;
        width: 100%;
    }
    .bttn {
    color: #ffff;
    background: #04AA6D;
    border: 2px solid #04AA6D;
    margin: 10px;
    text-align: center;
    font-family: sans-serif;
    padding: 10px;
    border-radius: 4px;
    float: right;
    cursor: pointer;
    }
</style>