<template>
  <div v-if="comments.length > 0" class="newsComment">
    <h2 class="text-center text-danger">Comments</h2>
    <transition-group name="list">
      <div class="comment d-flex" v-for="comment in comments" :key="comment.id">
        <div class="commentPost">
          <div><strong>Name:</strong> {{ comment.name }}</div>
          <div><b>body:</b> {{ comment.body }}</div>
          <div><b>email:</b> {{ comment.email }}</div>
        </div>
        <div class="d-flex">
          <button
            class="btn btn-secondary"
            @click="$router.push(`/comment/${comment.id}`)"
          >
            Open
          </button>
          <button class="btn btn-delete" @click="$emit('remove', comment)">
            Delete
          </button>
        </div>
      </div>
    </transition-group>
  </div>

  <div v-else>
    <h2 class="text-center text-danger">We can't any comments</h2>
  </div>
</template>

<script>
export default {
  props: {
    comments: {
      type: Array,
    },
  },
};
</script>

<style scoped>

.comment {
  margin-top: 10px;
  margin-bottom: 10px;
  padding: 10px;
  border-radius: 4px;
  background: #ffff;
  border: 1px solid rgb(146, 141, 141);
  display: flex;
  align-items: center;
  justify-content: space-between;

}
button{
    margin-left: 10px;
}
.commentPost{
    
    margin-right: 10px;
}
.btn-delete {
  color: #ffff;
  background: rgb(201, 6, 6);
  border: 2px solid rgb(201, 6, 6);
  text-align: center;
  font-family: sans-serif;
  padding: 5px 20px;
  border-radius: 4px;
  cursor: pointer;
}
.list-item {
  display: inline-block;
  margin-right: 10px;
}
.list-enter-active,
.list-leave-active {
  transition: all 1s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
.list-move {
  transition: transform 0.8s ease;
}
</style>
