<script>
    import { Router, Link, Route } from '@reach/router';
    import Navbar from './Navbar.svelte'; // You can create a separate Navbar component
    import Login from './Login.svelte';
    import Register from './Register.svelte';
    import BlogList from './BlogList.svelte';
    import CreateBlog from './CreateBlog.svelte';
  </script>
  
  <Router>
    <div>
      <Navbar />
  
      <Route path="/login" component={Login} />
      <Route path="/register" component={Register} />
      <Route path="/" component={BlogList} /> 
      <Route path="/create" component={CreateBlog} />
    </div>
  </Router>
  