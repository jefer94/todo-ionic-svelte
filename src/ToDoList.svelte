<script context="module">
  let autoIncrementToDoId = 0

  export function incrementToDoId() {
    return ++autoIncrementToDoId
  }

  export function addToDoItem(id, label) {
    return {id, label}
  }
</script>

<script>
  import Alert from './alert'
  import lang from './lang'

  export let items = []

  let listEvent = true
  let cache = items
  let input = ''
  let path = ''

  function addFromCache(id, label) {
    items = [].concat(items, addToDoItem(id, label))
    console.log(items)
    listEvent = true
    Alert(lang.createMessage, 'success')
  }

  function removeFromCache(id) {
    items = items.filter(v => v.id !== id)
    listEvent = true
    Alert(lang.removeMessage, 'danger')
  }
</script>

<ion-item>
  <ion-label position="floating">{lang.new}</ion-label>
  <ion-input on:change={v => input = v.target.value}></ion-input>
</ion-item>
<ion-button expand="block" on:click={() => addFromCache(incrementToDoId(), input)}>{lang.add}</ion-button>

<ion-list>
  {#each items as item}
    <ion-item>
      <ion-label>{item.label}</ion-label>
      <ion-badge slot="end" color="danger" on:click={() => removeFromCache(item.id)}>{lang.remove}</ion-badge>
    </ion-item>
  {/each}
</ion-list>
<!-- 
<choco-clock></choco-clock> -->
