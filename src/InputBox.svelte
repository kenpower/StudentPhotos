<script>
    const{ getPhotos} = $props();
  
    let inputText = "";
</script>
  
  <style>
    .container {
      display: flex;
      flex-direction: column;
      align-items: center;
      text-align: center;
      gap: 8px;
    }
  
    textarea {
      width: 100%;
      height: 100px;
      resize: vertical;
    }
  
    button {
      padding: 8px 16px;
      background-color: #007bff;
      color: white;
      border: none;
      cursor: pointer;
      border-radius: 4px;
    }
  
    button:hover {
      background-color: #0056b3;
    }
  </style>
  
  <div class="container">
    <textarea bind:value={inputText} placeholder="Enter list of students here, each entry should contain the student id (C00001234)..."></textarea>
    <button onclick={()=>getPhotos(inputText)}>Get Photos</button>
  </div>