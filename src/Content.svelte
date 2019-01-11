<div class="content">
{#if post}
  <div class="question">
    <h1>{@html question.title}</h1>
    <main>
      {@html question.content}
    </main>
  </div>

  {#if answer}
  <div class="answer">
    <h2>Student Answer</h2>
    {@html answer.history[0].content}
  </div>
  {/if}

  {#each comments as comment}
  <Comment {comment} />
  {/each}
{:else}
  No post is selected
{/if}
</div>

<script>
export default {
  components: {
    Comment: './Comment.svelte',
  },

  computed: {
    question: ({ post }) => ({
      title: post.history[0].subject,
      content: post.history[0].content,
    }),
    answer: ({ post }) => post.children.find(child => child.type === 's_answer'),
    comments: ({ post }) => post.children.filter(child => child.type === 'followup'),
  },
}
</script>

<style>
.content {
  box-sizing: border-box;
  flex-grow: 1;
  padding: 0 32px;
  height: calc(100vh - 40px);
  overflow-y: scroll;
}

.question, .answer {
  border: 1px solid #eeeeee;
  padding: 32px;
  margin: 16px 0;
}

</style>
