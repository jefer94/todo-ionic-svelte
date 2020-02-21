<script>
  let date = getDate();

  setInterval(() => this.date = this.getDate(), 1000)

  function getDate() {
    return moment().format('HH:mm:ss')
  }
</script>
<!-- 
<svelte:options tag="choco-clock">
  {this.date}
</svelte:options> -->