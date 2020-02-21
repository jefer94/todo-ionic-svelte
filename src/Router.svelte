<script context="module">
  export function addRoute(url, label, component) {
    return {url, label, component}
  }

  export function loadUrl(url, title, data = {}) {
    history.pushState(data, title, url)
  }
</script>

<script>
	import { afterUpdate } from 'svelte';

  let path = ''
  let result = []
  let howMany = 0
  export let routes = []

  console.log('a', routes)

  setInterval(() => {
    if (location.pathname !== path) {
      path = location.pathname

      result = routes.filter(({url}) => url === path).map(({component}) => component)

      let cache = result.length
      howMany = cache

      setTimeout(() => {
        for (let component of result)
          console.log(routes, result, typeof component, component)
        
        for (let component of result)
          new component({target: '#router-content-' + cache--})
      }, 1000);
      console.log(routes, result)
    }
  }, 0)

  function getId() {
    return 'router-content-' + howMany--
  }
</script>

{#each result as item}
  <!-- {item} -->
  <div id={getId()}></div>
{/each}