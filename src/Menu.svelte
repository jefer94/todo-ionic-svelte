<script>
  import Router, { loadUrl } from './Router.svelte'
  import lang from './lang'

  export function addMenuItem(url, label) {
    return {url, label}
  }

  function closeMenu() {
    // const menuCtrl = document.querySelector('ion-menu-controller')
    // menuCtrl.close()
  }
  export let routes = []
  export let title = ''
  export let color = 'tertiary'

  console.log(routes)
</script>

<style>
  .content {
    padding-top: 64px;
    cursor: pointer;
    z-index: 1;
  }
</style>
<!-- <link href="./core.css" type="stylesheet"/> -->
<ion-menu side="start" id="first" contentId="content-menu">
  <ion-header>
    <ion-toolbar color={color}>
      <ion-title>{lang.menu}</ion-title>
    </ion-toolbar>
  </ion-header>
  <ion-content>
    {#each routes as v}
      <ion-list>
        <ion-item on:click={() => {loadUrl(v.url, v.label); closeMenu();}}>{v.label}</ion-item>
      </ion-list>
    {/each}
  </ion-content>
</ion-menu>


<ion-header>
  <ion-toolbar color="tertiary">
    <ion-buttons slot="start">
      <ion-back-button></ion-back-button>
      <ion-menu-button></ion-menu-button>
    </ion-buttons>
  <ion-title>{title}</ion-title>
  </ion-toolbar>
</ion-header>


<ion-router-outlet id="content-menu" class="content" contentId="content-menu" main>
  <!-- <Router routes={routes}></Router> -->
  <slot></slot>
</ion-router-outlet>