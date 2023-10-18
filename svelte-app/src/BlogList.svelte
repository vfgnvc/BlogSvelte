<script>
    import { onMount } from 'svelte';
    import { navigate } from '@reach/router';
    let blogs = [];
    let currentPage = 1;
    let loading = true;
    let error = null;
  
    const API_BASE_URL = 'http://localhost:3001/blogs';
  
    async function fetchBlogs() {
      try {
        const response = await fetch(API_BASE_URL);
        if (response.ok) {
          blogs = await response.json();
        } else {
          error = 'Error fetching blog details';
        }
        loading = false;
      } catch (err) {
        error = 'Error fetching blog details';
        loading = false;
      }
    }
  
    onMount(() => {
      // Fetch blogs when the component mounts
      fetchBlogs();
    });
  
    function handleNextPage() {
      currentPage += 1;
    }
  </script>
 
  <div>
    <div class="container">
      <div class="row mt-5">
        {#if loading}
          <div class="spinner-border" role="status">
            <span class="sr-only">Loading...</span>
          </div>
        {:else if error}
          <div class="alert alert-danger" role="alert">{error}</div>
        {:else}
          {#each blogs as blog (blog._id)}
            <div class="col-md-4 mb-4">
              <div class="card">
                <div class="card-body">
                  <h5 class="card-title">{blog.title}</h5>
                  <p class="card-text">{blog.content.substring(0, 100)}...</p>
                  <button class="btn btn-primary">Read More</button>
                </div>
              </div>
            </div>
          {/each}
        {/if}
      </div>
      <div class="row justify-content-center mt-3">
        <div class="col">
          <button class="btn btn-primary" on:click={handleNextPage}>Next Page</button>
        </div>
      </div>
    </div>
  </div>
