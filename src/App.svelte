<Header title="CS348 Piazza" />
<div class="content">
  <Sidebar posts={titles} selected={selected} on:select="changeQuestion(event.nr)"/>
  <Content post={posts.find(({ nr }) => nr === selected)} {students} />
</div>

<script>
import ALL_POSTS from '../cs348-fall-2017.json';

ALL_POSTS.sort((a, b) => b.result.nr - a.result.nr);

function getStudents(posts) {
  const students = [].concat(...posts.map(post => [].concat(post.tag_good || [], post.tag_endorse || [], getStudents(post.children))))

  const ids = new Set();

  for (const student of students) {
    const { id } = student;
  }

  return students.filter(({ id }) => {
    if (ids.has(id)) {
      return false;
    }
    ids.add(id);
    return true;
  });
}

export default {
  components: {
    Header: './Header',
    Sidebar: './Sidebar',
    Content: './Content',
  },

  methods: {
    changeQuestion(nr) {
      this.set({ selected: nr });
      window.location.hash = nr;
    }
  },

  computed: {
    titles: ({ posts }) => posts.map(({ nr, history: [{ subject }] }) => ({ nr, subject })),
    students: ({ posts }) => getStudents(posts)
      .reduce((acc, student) => Object.assign(acc, { [student.id]: student }), {}),
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
