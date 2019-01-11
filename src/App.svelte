<Header title="CS348 Piazza" />
<div class="content">
  <Sidebar posts={titles} selected={selected} on:select="set({ selected: event.nr })"/>
  <Content post={posts.find(({ nr }) => nr === selected)} />
</div>

<script>
import ALL_POSTS from '../cs348-fall-2017.json';

ALL_POSTS.sort((a, b) => b.result.nr - a.result.nr);

export default {
  components: {
    Header: './Header',
    Sidebar: './Sidebar',
    Content: './Content',
  },

  computed: {
    titles: ({ posts }) => posts.map(({ nr, history: [{ subject }] }) => ({ nr, subject })),
  },

  data() {
    return {
      posts: ALL_POSTS.map(({ result }) => result),
      selected: 28,
    }
  }
}
</script>

<style>
.content {
  display: flex;
  flex-direction: row;
}
</style>
