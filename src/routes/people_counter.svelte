<script>
  export let count = 0;
  console.log(count);

  function increment() {
    count += 1;
  }

  function decrement() {
    count -= 1;
  }
</script>

<div class="text-center">
  <div class="text-center text-2xl">
    People Entered: <br />
    {count}
  </div>
  <button
    on:click={increment}
    id="increment-btn"
    class="bg-success px-6 py-2 rounded-xl shadow-lg my-6">Add People</button
  >
  <button
    on:click={decrement}
    id="increment-btn"
    class="bg-red-500 px-6 py-2 rounded-xl shadow-lg my-6">Remove People</button
  >
</div>
