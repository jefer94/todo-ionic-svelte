<script>
	import Menu from './Menu.svelte'
	import TodoList from './TodoList.svelte'
	import { addRoute } from './Router.svelte'
	import lang from './lang'

	let path = ''
	let routes = [
		addRoute('/', lang.list, TodoList)
	]

	setInterval(() => {
    if (location.pathname !== path)
      path = location.pathname
  }, 0)
</script>

<app-root>
	<ion-app>
		<Menu color="tertiary" title={lang.list} routes={routes}>
		  {#if path === '/'}
			  <TodoList></TodoList>
			{/if}
		</Menu>
		<ion-router-outlet></ion-router-outlet>
	</ion-app>
</app-root>

<style>
</style>