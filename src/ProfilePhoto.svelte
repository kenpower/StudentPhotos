<script>
  const { imageUrl, label } = $props();
</script>

<div class="container">
  <img class="image" src={imageUrl} alt={label} />
  <div class="label">{label}</div>
</div>

<style>
  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    break-inside: avoid; /* Prevents splitting across pages */
  }

  .image {
    width: 100%;
    height: auto;
    border-radius: 50%;
    object-fit: cover;
  }

  .label {
    margin-top: 8px;
    font-size: 1rem;
    color: #333;
    word-wrap: break-word;
    overflow-wrap: break-word;
    max-width: 100%;
  }
</style>
