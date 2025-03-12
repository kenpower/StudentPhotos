<script>
  import svelteLogo from './assets/svelte.svg'
  import viteLogo from '/vite.svg'
  import Counter from './lib/Counter.svelte'
    import ProfilePhoto from './ProfilePhoto.svelte';
    import InputBox from './InputBox.svelte';

  let listOfStudents=$state(null)

  function getPhotos(text) {
    const pattern = /C\d{8}/g;
    const lines = text.split("\n");
    
    listOfStudents = lines.map(line => {
      const match = line.match(pattern);
      return {
        label: line + (match ? "" : "No valid ID found"),
        id: match ? match[0] : null,
        error: match ? null : "No valid ID found",
        imageUrl: `https://idpics-cw.setu.ie/${match}.jpg`
      };
    });
    
    console.log("Processed Data:", listOfStudents);
  }

  
</script>

<main>
Heading
  {#if listOfStudents}
   Photos
    {#each listOfStudents as {imageUrl , label} }
      <ProfilePhoto {imageUrl} {label}/>
    {/each}
  {:else}
    Input
    <InputBox {getPhotos}/>
  {/if}
</main>

<style>
  .logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
    transition: filter 300ms;
  }
  .logo:hover {
    filter: drop-shadow(0 0 2em #646cffaa);
  }
  .logo.svelte:hover {
    filter: drop-shadow(0 0 2em #ff3e00aa);
  }
  .read-the-docs {
    color: #888;
  }
</style>
