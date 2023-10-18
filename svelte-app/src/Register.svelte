<script>
    import { onMount } from 'svelte';
    import { navigate } from '@reach/router';
    let username = '';
    let password = '';
  
    const axiosInstance = axios.create({
      baseURL: 'http://localhost:3001',
    });
  
    async function handleRegister() {
      try {
        const response = await axiosInstance.post('/register', { username, password });
        console.log(response.data.message);
      } catch (error) {
        console.error('Registration failed:', error);
      }
    }
  </script>
  
  <div class="container">
    <div class="row justify-content-center mt-5">
      <div class="col-md-6">
        <h2 class="mb-4">Register</h2>
        <form>
          <div class="form-group">
            <label for="username">Username</label>
            <input
              type="text"
              class="form-control"
              id="username"
              placeholder="Enter username"
              bind:value={username}
            />
          </div>
          <div class="form-group">
            <label for="password">Password</label>
            <input
              type="password"
              class="form-control"
              id="password"
              placeholder="Enter password"
              bind:value={password}
            />
          </div>
          <button class="btn btn-primary" on:click={handleRegister}>Register</button>
        </form>
        <p class="mt-3">
          Already have an account? <a href="/login">Login</a>
        </p>
      </div>
    </div>
  </div>
  