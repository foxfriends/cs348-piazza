<div class="container">
  <input class="search" placeholder="Search" type="text" bind:value=filter />
  {#each filteredPosts as post}
  <div class="post" class:selected="post.nr === selected" on:click="fire('select', { nr: post.nr })">
    {@html post.subject}
  </div>
  {/each}
</div>

<script>
export default {
  computed: {
    filteredPosts: ({ posts, filter }) => filter
      ? posts.filter(post => post.subject.toLowerCase().includes(filter.toLowerCase()) || post.nr === +filter)
      : posts,
  },

  data() {
    return {
      filter: '',
    }
  }
}
</script>

<style>
.container {
  width: 300px;
  height: calc(100vh - 40px);
  overflow-y: scroll;
  border-right: 1px solid #EEEEEE;
}

.search {
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #EEEEEE;
  height: 30px;
  width: 100%;
  padding: 0 16px;
  margin: 0;
}

.post {
  display: flex;
  flex-direction: column;
  justify-content: center;
  border-bottom: 1px solid #EEEEEE;
  height: 40px;
  padding: 0 16px;
  cursor: pointer;
  font-size: smaller;
  font-weight: 600;
}

.post:hover {
  background-color: #FAFAFA;
}

.selected, .selected:hover {
  background: #F0F0F0;
}
</style>
