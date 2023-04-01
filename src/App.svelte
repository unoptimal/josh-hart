<script>
  import HighFives from "./lib/HighFives.svelte";
  
  import { onMount } from "svelte";
  import * as d3 from "d3";


  let data;

  onMount(async () => {
    data = await d3.csv("./highfives.csv");
  });
  
</script>

<h1 style='font-size: 3rem'>Josh Hart High Five Tracker</h1>
<p style='text-align:center'><i>by <a href="https://unoptimal.com/">unoptimal</a></i></p>
<p style='text-align:center'><i>Last updated March 31, 2023</i><p>


<img src="hart.jpg" alt="josh hart high 5">

<div class='container'>
  <p>NBA player <a href='https://en.wikipedia.org/wiki/Josh_Hart'>Josh Hart</a> seemingly just cannot get a high five from his peers - <a href="https://www.silverscreenandroll.com/2018/12/12/18137355/laker-film-room-josh-hart-lakers-worst-player-high-fives-nba-history-video-twitter-breakdown">though it might partially be his fault</a>. Either way, I gathered every recorded missed high five I could find online.</p>
  <p>Note: I am currently missing a better clip for Julius Randle's missed high five at 0:40 in <a href='https://www.youtube.com/watch?v=CBYiqyRmRNg'>this video</a>. Reach out if you find one.</p>
  <i><p>Missing a high five? Other comments or suggestions? Let me know at <a href='https://twitter.com/thatsnotoptimal'>@thatsnotoptimal</a> or <a href='https://www.reddit.com/u/unoptimalblogs'>u/unoptimalblogs</a>. View the source code for this project <a href="https://github.com/unoptimal/josh-hart-tracker">here</a>.</p></i>
</div>

  {#if data}
    <HighFives data={data}/>
  {:else}
    <p>Loading data...</p>
  {/if}
<style>

  img {
    display: block;
    margin-left: auto;
    margin-right: auto;
    max-width: 300px;
    margin-bottom: 10px;
  }

  h1 {
    text-align: center;
  }


  .container {
    display: flex;
    align-items: center;
    flex-direction: column;
    margin: 0 auto;
    max-width: 600px;
}
@media (max-width: 768px) {
    .container {
      max-width: 300px;
    }
  }

</style>