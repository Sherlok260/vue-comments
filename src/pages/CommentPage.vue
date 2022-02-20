<template>
  <div class="main">
    <!-- <button class="btn" @click="fetchComments">Show all info</button> -->
    <my-modal v-model:show="modalVisible">
      <comment-form @createComment="createComment"/>
    </my-modal>
    <div class="d-inline-flex">
      <input class="form-control" type="text" v-model="searchQuery" placeholder="Search...">
      <my-select class="w-25 btn" v-model="selectedSort" :selectOptions="selectOptions"/>
      <button @click="showModal" class="btn btn-primary text-decoration-none">Add</button>
    </div>
    <comment-list :comments="sortedAndSearchComments" @remove="commentRemove" v-if="!isLoading"/>
    <div v-else>
      <div class="spinner-grow col-md-3 offset-md-6" role="status">
        <span class="sr-only">Loading...</span>
      </div> 
    </div>
    <div class="page_wrapper container">
      <div class="btn btn-primary mx-1" :class="{'current-page' : page === pageNum}" v-for="pageNum in totalPage" @click="changePage" :key="pageNum.id">
        {{ pageNum }}
      </div>
    </div>
  </div>
</template>

<script>
import CommentForm from '@/components/CommentForm'
import CommentList from '@/components/CommentList'
import Navbar from '@/components/Navbar'
import axios from 'axios'

export default {
  components: {
    CommentForm,
    CommentList,
    Navbar
  },
  data(){
    return {
      comments: [],
      modalVisible: false,
      isLoading: false,
      searchQuery: "",
      selectedSort: "",
      totalPage: 0,
      page: 1,
      limit: 50,
      selectOptions: [
        {value: "name", name: "Filter by name"},
        {value: "email", name: "Filter by email"}
      ]
    }
  },
  methods: {
    createComment(comm) {
      this.comments.push(comm),
      this.modalVisible = false
    },
    commentRemove(comment) {
      this.comments = this.comments.filter(c => c.id !== comment.id)
    },
    showModal() {
      this.modalVisible = !this.modalVisible
    },
    changePage(){
      this.page = this.page + 1;
      this.fetchComments();
    },
    async fetchComments(){
      try {
        this.isLoading = true;
        const response = await axios.get('https://jsonplaceholder.typicode.com/comments', {
          params: {
            _limit: this.limit,
            _page: this.page
          }
        });
        this.totalPage = Math.ceil(response.headers['x-total-count'] / this.limit);
        console.log(response.data);
        this.comments = response.data;
      } catch(e) {
        alert(e);
      } finally {
        this.isLoading = false;
      }
    }
  },
  mounted() {
    this.fetchComments();
  },
  computed: {
    filteredComments() {
      return [...this.comments].sort((a,b)=> {
        if(this.selectedSort === "name") {
          return a.name.localeCompare(b.name);
        } else if(this.selectedSort === "email") {
          return a.email.localeCompare(b.email);
        }
      });
    },
    sortedAndSearchComments() {
      return this.filteredComments.filter(comment => {
        return comment.name.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
          comment.email.toLowerCase().includes(this.searchQuery.toLowerCase());
      });
    }
  },
  // watch: {
  //   selectedSort(newValue) {
  //     this.comments.sort((comm1,comm2)=> {
  //       if(newValue === "name"){
  //         return comm1.name.localeCompare(comm2.name);
  //       } else if(newValue === "email") {
  //         return comm1.email.localeCompare(comm2.email);
  //       }
  //     });
  //   }
  // }
}
</script>

<style>
  .main {
    margin: 20px 100px auto;
    padding: 50px;
    display:grid;
  }
  .current-page {
    background-color: #fff;
    color: #000;
  }
</style>
