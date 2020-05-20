<script>
  let password = ''

  const hash = s =>
    s.split('').reduce((a, b) => {
      a = (a << 5) - a + b.charCodeAt(0)
      return a & a
    }, 0)

  // $: console.log(password, hash(password))
  $: isProd = process.env.isProd
  $: isProd
</script>

<style>
  div {
    font-family: sans-serif;
    font-size: 12px;
    margin-left: 50%;
    width: 400px;
    margin-top: 100px;
  }

  label {
    font-weight: bold;
  }

  input[type='password'] {
    width: 200px;
  }
</style>

{#if !isProd || hash(password) === -791498901}
  <slot />
{:else}
  <div>
    <label for="password">Password:</label>
    <input id="password" bind:value={password} type="password" />
  </div>
{/if}
