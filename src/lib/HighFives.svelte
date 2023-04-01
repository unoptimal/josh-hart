<script>
  export let data;
  import { Accordion, AccordionItem } from 'svelte-collapsible';
</script>

<div class='container'>
  
  {#if data}
    
    <h1 style='margin-bottom: -10px; text-align: center'>Most recent time left hanging:</h1>
    <h2>{new Date(data[0].date).toLocaleDateString('en-US', { month: 'long', day: 'numeric', year: 'numeric' })} - {data[0].player}</h2>
    
    {#if data[0].link.includes('streamable.com')}
      <div class='streamable'>
        <iframe title='lead' width="100%" height="100%" src={data[0].link.replace('streamable.com/', 'streamable.com/e/') + '?loop=0'} frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture; fullscreen"  style="position: absolute; top: 0px; left: 0px; width: 100%; height: 100%;"><small>Powered by <a href="https://embed.tube/embed-code-generator/streamable/">streamable embed</a> generator</small></iframe>
      </div>
      
      {:else if data[0].link.includes('youtube.com')}
      <div class='youtube'>
        <iframe width="473" height="841" src={data[0].link.replace('youtube.com/shorts/', 'youtube.com/embed/')} title='youtube-link' frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
      </div>

      
      {:else if data[0].link.includes('twitter.com')}
      <div class='twitter'>
        <blockquote class="twitter-video"><a href="${data[0].link}"></a></blockquote><script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>;
      </div>
    {/if}

    <h1>Previous Instances:</h1>
    <Accordion>
      
      { #each data.slice(1) as item, index }
      <AccordionItem key={index}>
          
        <div slot='header' class='header'>
          <div>
            <h2>{new Date(item.date).toLocaleDateString('en-US', { month: 'long', day: 'numeric', year: 'numeric' })} - {item.player}</h2>
          </div>
        </div>
        
        <p slot='body' class='body'>
          {#if item.link.includes('streamable.com')}
            <div class='streamable'>
              <iframe title='lead' width="100%" height="100%" src={item.link.replace('streamable.com/', 'streamable.com/e/') + '?loop=0'} frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture; fullscreen"  style="position: absolute; top: 0px; left: 0px; width: 100%; height: 100%;"><small>Powered by <a href="https://embed.tube/embed-code-generator/streamable/">streamable embed</a> generator</small></iframe>
            </div>

          {:else if item.link.includes('youtube.com')}
            <div class='youtube'>
              <iframe width="100%" height="841px" src={item.link.replace('youtube.com/shorts/', 'youtube.com/embed/')} title='youtube-link' frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
            </div>
          {:else if item.link.includes('twitter.com')}
            <blockquote class="twitter-video"><a href="${item.link}"></a></blockquote><script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
          {/if}
        </p>

      </AccordionItem>
    { /each }
    </Accordion>
  {/if}
</div>

<style>

.streamable {
  padding-bottom: 56.25%;
  position: relative;
}

.youtube{
  max-width: 2000px;
}

  .container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    margin: 0 auto;
    max-width: 800px;
  }

  h1, h2 {
    text-align: center;
  }

  .header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
    background-color: #f5f5f5;
  }

  .body {
    padding: 10px;
    border: 1px solid #ddd;
    margin-bottom: 10px;
  }

</style>