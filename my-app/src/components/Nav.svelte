<script>
  import { Router, Link, Route } from "svelte-routing";
  // import Home from "../routes/Home.svelte";
  import Home from "../routes/Home.svelte";
  import About from "../routes/About.svelte";
 

  export let url = "";
</script>

<Router url="{url}">
  <nav>
    <Link to="/">Home</Link>
    <span> | </span>
    <Link to="about">About</Link>
   
  </nav>
  <div>
    
    <Route path="about" component="{About}" />
    <Route path="/" component="{Home}"></Route>
  </div>
</Router>