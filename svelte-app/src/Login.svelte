<script>
    import { onMount } from 'svelte';
    import { navigate } from '@reach/router';
    let username = '';
    let password = '';
  
    async function handleLogin() {
      try {
        const response = await fetch('http://localhost:3001/login', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify({ username, password }),
        });
        if (response.ok) {
          const result = await response.json();
          if (result === 'Success') {
            navigate('/create');
          }
        } else {
          console.error('Login failed:', response.statusText);
        }
      } catch (error) {
        console.error('Login failed:', error);
      }
    }
  </script>
  
  <main>
      <div class="container">
          <div class="row justify-content-center mt-5">
            <div class="col-md-6">
              <h2 class="mb-4">Login</h2>
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
                <button class="btn btn-primary" on:click={handleLogin}>Login</button>
              </form>
              <p class="mt-3">
                Don't have an account? <a href="/register">Register</a>
              </p>
            </div>
          </div>
        </div>
  </main>
  
  