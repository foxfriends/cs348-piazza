<div class="comment">
  <span class="author">
    {comment.anon !== 'no' ? 'Anonymous:' : 'Someone:'}
  </span>
  {@html comment.subject}

  {#each comment.children as response}
  <div class="response">
    <span class="author">
      {response.anon !== 'no' ? 'Anonymous:' : 'Someone:'}
    </span>
    {@html response.subject}
  </div>
  {/each}
</div>

<style>
.author {
  color: #666;
  font-size: smaller;
}

.comment, .response {
  box-sizing: border-box;
  padding: 16px;
  margin: 16px 0;
  border: 1px solid #eeeeee;
  width: 100%;
}
</style>
