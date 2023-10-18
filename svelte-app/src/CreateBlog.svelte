<script>
    import { onMount } from 'svelte';
    import { navigate } from '@reach/router';
    let newBlogTitle = '';
    let newBlogContent = '';
    let redirect = false;
  
    async function handleCreateBlog() {
      try {
        const response = await fetch('http://localhost:3001/create-blog', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify({ title: newBlogTitle, content: newBlogContent }),
        });
        if (response.ok) {
          const result = await response.json();
          console.log(result.message);
          redirect = true;
        }
        newBlogTitle = '';
        newBlogContent = '';
      } catch (error) {
        console.error('Blog creation failed:', error);
      }
  
      if (redirect) {
        navigate('/');
      }
    }
  </script>
  
  <div class="container mt-5">
    <div class="col-md-6">
      <h2>Create a New Blog</h2>
      <form>
        <div class="form-group">
          <label for="newBlogTitle">Title</label>
          <input
            type="text"
            class="form-control"
            id="newBlogTitle"
            placeholder="Enter title"
            bind:value={newBlogTitle}
          />
        </div>
        <div class="form-group">
          <label for="newBlogContent">Content</label>
          <textarea
            class="form-control"
            id="newBlogContent"
            rows="4"
            placeholder="Enter content"
            bind:value={newBlogContent}
          ></textarea>
        </div>
        <button class="btn btn-success" on:click={handleCreateBlog}>Create Blog</button>
      </form>
    </div>
  </div>
  