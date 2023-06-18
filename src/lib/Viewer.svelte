<script>
 import { onMount, afterUpdate } from 'svelte';

 let logText = `2023-06-18 10:00:00 - Application started\n2023-06-18 10:01:23 - Processing data...\n2023-06-18 10:02:15`;

 let containerElement;
 let isScrolledToBottom = true;

  onMount(() => {
    scrollContainerToBottom();
  });

  afterUpdate(() => {
    if (isScrolledToBottom) {
      scrollContainerToBottom();
    }
  });

  function scrollContainerToBottom() {
    containerElement.scrollTop = containerElement.scrollHeight;
  }

  function handleScroll() {
    const { scrollTop, scrollHeight, clientHeight } = containerElement;
    isScrolledToBottom = scrollTop + clientHeight >= scrollHeight - 10;
  }
</script>

<div
  class="log-viewer"
  on:scroll={handleScroll}
  bind:this={containerElement}
>
    <pre class="log-text">{logText}</pre>
</div>

<style>
 .log-viewer {
     height: 400px;
     overflow-y: auto;
     background-color: #f1f1f1;
     border: 1px solid #ccc;
     padding: 10px;
     font-family: monospace;
 }

 .log-text {
     white-space: pre-wrap;
     margin: 0;
 }
</style>
