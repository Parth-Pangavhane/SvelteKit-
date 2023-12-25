<script>
    export let id; // Add an ID prop to uniquely identify each sticky note
    let color = 'yellow';
    let shape = 'rectangle';
    let content = '';
  
    let dragging = false;
    let offsetX = 0;
    let offsetY = 0;
  
    function handleMouseDown(event) {
      dragging = true;
      offsetX = event.clientX - event.target.offsetLeft;
      offsetY = event.clientY - event.target.offsetTop;
    }
  
    function handleMouseMove(event) {
      if (dragging) {
        event.preventDefault();
        const x = event.clientX - offsetX;
        const y = event.clientY - offsetY;
        event.target.style.left = `${x}px`;
        event.target.style.top = `${y}px`;
      }
    }
  
    function handleMouseUp() {
      dragging = false;
    }
    
 
    


   

  
  </script>
  
  
  
  
  
  <div
    class="sticky-note"
    bind:this={id}
    on:mousedown={handleMouseDown}
    on:mousemove={handleMouseMove}
    on:mouseup={handleMouseUp}
    style="background-color: {color}; border: 2px solid black; border-radius: {shape === 'circle' ? '50%' : '0%'}"
  >
    <div class="controls">
      <label>
        Color:
        <input type="color" bind:value={color} />
      </label>
      <label>
        Shape:
        <select bind:value={shape}>
          <option value="rectangle">Rectangle</option>
          <option value="circle">Circle</option>
        </select>
      </label>
    </div>
    <textarea
      bind:value={content}
      placeholder="Write something..."
      style="width: 100%; height: calc(100% - 50px); border: none; background-color: transparent; resize: none; font-size: 1rem;"
    ></textarea>
  </div>
  

  <style>
    .sticky-note {
      position: absolute;
      width: 200px;
      height: 200px;
      padding: 1rem;
      margin: 1rem;
      cursor: move;
      background-color: #ffd700; /* Yellow */
      border: 2px solid #333; /* Dark border */
      border-radius: 10px; /* Rounded corners */
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); /* Shadow */
      z-index: 1;
      transition: transform 0.2s ease;
      overflow: hidden; /* Ensure content doesn't overflow rounded corners */
      font-family: 'Arial', sans-serif;
    }
  
    .sticky-note textarea {
      height: 100%;
      border: none;
      background-color: transparent;
      resize: none;
      font-size: 1rem;
      width: 100%;
      box-sizing: border-box; /* Ensure padding is included in width */
      color: #333; /* Dark text color */
      font-family: inherit;
    }
  
    .controls {
      display: flex;
      justify-content: space-between;
      margin-top: 0.5rem;
    }
  
    .controls label {
      font-weight: bold;
    }
  
    .controls input[type="color"],
    .controls select {
      border: none;
      background: none;
      font-size: 1rem;
      margin-left: 0.51rem;
    }
  
    .controls select {
      font-family: inherit;
      cursor: pointer;
    }
  
    
    

  </style>
  
  
  
  
