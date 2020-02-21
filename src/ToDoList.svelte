<script context="module">
  const key = '__TO_DO_LAST_ID__'
  const store = JSON.parse(localStorage.getItem(key) || '0')
  let autoIncrementToDoId = store

  export function incrementToDoId() {
    localStorage.setItem(key, ++autoIncrementToDoId)
    return autoIncrementToDoId
  }

  export function addToDoItem(id, label) {
    return {id, label}
  }
</script>

<script>
  import Alert from './alert'
  import lang from './lang'

  const key = '__TO_DO_ITEMS__'
  const storeItems = JSON.parse(localStorage.getItem(key) || '[]')

  export let items = storeItems

  let listEvent = true
  let cache = items
  export let input = ''
  let path = ''

  function addFromCache(id, label) {
    document.querySelector('#input').value = ""
    items = [].concat(items, addToDoItem(id, label))
    
    localStorage.setItem(key, JSON.stringify(items))

    listEvent = true
    Alert(lang.createMessage, 'success')
  }

  function removeFromCache(id) {
    input = ''
    items = items.filter(v => v.id !== id)

    localStorage.setItem(key, JSON.stringify(items))

    listEvent = true
    Alert(lang.removeMessage, 'danger')
  }
</script>

<style>
  .list {
    max-width: 500px;
    width: 100vw;
  }

  .list-wrapper {
    display: flex;
    width: 100vw;
    height: calc(100vh - 64px);
    overflow-y: auto;
    justify-content: center;
  }
</style>

<div class="list-wrapper">
  <div class="list">
    <ion-item>
      <ion-label position="floating">{lang.new}</ion-label>
      <ion-input on:change={v => input = v.target.value} id="input"></ion-input>
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
  </div>
</div>