<script>
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
        imageUrl: match ? `https://idpics-cw.setu.ie/${match}.jpg`: "./no_profile_pic.png",
      };
    });
    
    console.log("Processed Data:", listOfStudents);
  }

  
</script>

<main>
<h1>Paste list from... (e.g. from excel)</h1>>
  {#if listOfStudents}
   Photos
   <div class="grid">
    {#each listOfStudents as {imageUrl , label} }
    <div class="grid-item">
      <ProfilePhoto {imageUrl} {label}/>
    </div>
    {/each}
  </div>
  {:else}
    Input
    <InputBox {getPhotos}/>
  {/if}
</main>

<style>
 .grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
    gap: 10px;
    margin-top: 20px;
    width: 100%;
    max-width: 100%;
    overflow-x: hidden;
  }

  .grid-item {
    padding: 10px;
    border: 1px solid #ccc;
    text-align: center;
  }
</style>
