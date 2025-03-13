<script>
  import ProfilePhoto from "./ProfilePhoto.svelte";
  import InputBox from "./InputBox.svelte";

  let listOfStudents = $state(null);

  let columns = $state(4); // Default number of columns
  let gapSize = $state(10); // Default gap size

  function getPhotos(text) {
    const pattern = /[Cc]\d{8}/g;
    const lines = text.split("\n");

    const filteredLines = lines.filter((line) => line.trim() !== "");

    listOfStudents = filteredLines.map((line) => {
      const match = line.match(pattern);

      if (line.trim() === "")
        return {
          label: line,
          id: null,
          error: null,
          imageUrl: "./no_profile_pic.png",
        };
      return {
        label: line + (match ? "" : "No valid ID found"),
        id: match ? match[0] : null,
        error: match ? null : "No valid ID found",
        imageUrl: match
          ? `https://idpics-cw.setu.ie/${match[0].toUpperCase()}.jpg`
          : "./no_profile_pic.png",
      };
    });

    console.log("Processed Data:", listOfStudents);
  }
</script>

<main>
  {#if listOfStudents}
    <div class="no-print">
      <label for="columns">Columns: {columns}</label>
      <input id="columns" type="range" min="1" max="8" bind:value={columns} />

      <label for="gapSize">Gap Size: {gapSize}px</label>
      <input id="gapSize" type="range" min="0" max="100" bind:value={gapSize} />
    </div>
    <div class="grid" style="--columns: {columns}; --gap-size: {gapSize}px;">
      {#each listOfStudents as { imageUrl, label }}
        <div class="grid-item">
          <ProfilePhoto {imageUrl} {label} />
        </div>
      {/each}
    </div>
  {:else}
    <h1>Paste list from... (e.g. from excel)</h1>
    Input
    <InputBox {getPhotos} />
  {/if}
</main>

<style>
  :root {
    --columns: 4; /* Default number of columns */
  }

  .grid {
    display: grid;
    grid-template-columns: repeat(var(--columns), 1fr);
    gap: var(--gap-size, 10px);
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

  @media print {
    ::-webkit-scrollbar {
      display: none; /* Hides scrollbars in WebKit browsers */
    }

    .no-print {
      display: none !important;
    }

    body {
      overflow: hidden; /* Prevents scrolling */
    }
  }
</style>
