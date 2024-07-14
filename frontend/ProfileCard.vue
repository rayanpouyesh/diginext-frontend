<template>
  <div class="profile-card">
    <h2>{{ profile.name }}</h2>
    <p>{{ profile.specialty }}</p>
    <p>Likes: {{ profile.likes }}</p>
    <div>
      <textarea v-model="newComment" placeholder="Write a comment..."></textarea>
      <button @click="addComment">Add Comment</button>
    </div>
    <ul>
      <li v-for="comment in profile.comments" :key="comment.id">{{ comment.text }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    profile: Object
  },
  data() {
    return {
      newComment: ''
    };
  },
  methods: {
    addComment() {
      if (this.newComment.trim() !== '') {
        this.$emit('add-comment', this.profile.id, this.newComment);
        this.newComment = '';
      }
    }
  }
};
</script>

<style>
.profile-card {
  border: 1px solid #ccc;
  padding: 10px;
  margin: 10px;
}
</style>
