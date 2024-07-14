<template>
  <div id="app">
    <button @click="sortAsc">Sort by Likes Ascending</button>
    <button @click="sortDesc">Sort by Likes Descending</button>
    <div v-for="profile in sortedProfiles" :key="profile.id">
      <ProfileCard :profile="profile" @add-comment="addComment" />
    </div>
  </div>
</template>

<script>
import ProfileCard from './components/ProfileCard.vue';

export default {
  name: 'App',
  components: {
    ProfileCard
  },
  data() {
    return {
      profiles: [
        { id: 1, name: 'Dr. Smith', specialty: 'Cardiology', likes: 10, comments: [] },
        { id: 2, name: 'Dr. Johnson', specialty: 'Neurology', likes: 5, comments: [] },
        { id: 3, name: 'Dr. Lee', specialty: 'Orthopedics', likes: 8, comments: [] }
        // سایر پروفایل‌ها
      ],
      sortOrder: 'asc' // یا 'desc'
    };
  },
  computed: {
    sortedProfiles() {
      return this.profiles.sort((a, b) => {
        if (this.sortOrder === 'asc') {
          return a.likes - b.likes;
        } else {
          return b.likes - a.likes;
        }
      });
    }
  },
  methods: {
    sortAsc() {
      this.sortOrder = 'asc';
    },
    sortDesc() {
      this.sortOrder = 'desc';
    },
    addComment(profileId, commentText) {
      const profile = this.profiles.find(p => p.id === profileId);
      if (profile) {
        profile.comments.push({ id: Date.now(), text: commentText });
      }
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
}
</style>
