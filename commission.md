---
layout: page
title: Custom Commissions
subtitle: Digital Art and Fursuits :D
---
Art commissions can be found on <a href="https://ko-fi.com/redrileypcreates">ko-fi</a>, fursuit commissions are **CLOSED** but you can calculate a free estimate[^1] below.
#### Features included in base price:
- Up to 3 fur colors
- Short or average length tail
- Magnetic eyelids
- Cotton lining
- Custom 3D-printed headbase (in PLA, static jaw)
- Simple markings

[^1]: Quotes are not a final price and are subject to change! Reach out to get an accurate price for a commission.

<!-- HTML Structure -->
<div id="quote-calculator">
  <h3>Get an Instant Quote </h3>
  <!-- Fursuit Type -->
  <label for="service-type">Select Fursuit Type:</label>
  <select id="service-type">
    <option value="800">Head ($800)</option>
    <option value="1300">Mini Partial ($1300)</option>
    <option value="1700">Full Partial ($1700)</option>
  </select>

  <!-- Tail Length: Initially Hidden -->
  <div id="tailLengthWrapper" class="hidden">
    <label for="tailLength">Tail Length:</label>
    <select id="tailLength">
      <option value="0">Short (<= 1ft>)</option>
      <option value="0">Average (1ft-3ft)</option>
      <option value="250">Long (3ft+)</option>
      <option value="500">Floor-dragger</option>
    </select>
  </div>

  <!-- Marking Complexity -->
  <label for="markingComplexity">Select Marking Complexity:</label>
  <select id="markingComplexity">
    <option value="0">Simple patterns</option>
    <option value="150">Moderate patterns</option>
    <option value="300">Complex patterns/some asymmetry</option>
    <option value="500">High detail/full asymmetry</option>
  </select>

  <!-- Number of Colors -->
  <label for="colors">Number of Colors:</label>
  <input type="range" id="colors" value="1" min="1" max="8" oninput="this.nextElementSibling.value = this.value">
  <output>1</output>

  <!-- Additional Features -->
  <label for="addlFeatures">Select Additional Features:</label>
  <div>
    <input type="checkbox" id="tpu" name="addlFeatures" value="tpu">
    <label for="tpu">TPU instead of PLA (+$40)</label>
  </div>
  <div>
    <input type="checkbox" id="squeaker" name="addlFeatures" value="squeaker">
    <label for="squeaker">Squeakers in paws/nose/tail (+$20)</label>
  </div>
  <div>
    <input type="checkbox" id="nfc" name="addlFeatures" value="nfc">
    <label for="nfc">Programmable NFC tag in nose (+$10)</label>
  </div>
  <div>
    <input type="checkbox" id="horns" name="addlFeatures" value="horns">
    <label for="horns">3D-printed horns (+$100)</label>
  </div>
  <div>
    <input type="checkbox" id="fan" name="addlFeatures" value="fan">
    <label for="fan">Head fan (+$50)</label>
  </div>
  <div>
    <input type="checkbox" id="jaw" name="addlFeatures" value="jaw">
    <label for="jaw">Moveable jaw (+$100)</label>
  </div>

  <div class="result">
    Estimated Price: <span id="total-price">$800.00</span>
  </div>
</div>

<!-- JavaScript Logic -->
<script>
  const serviceSelect = document.getElementById('service-type');
  const colorsInput = document.getElementById('colors');
  const totalPriceDisplay = document.getElementById('total-price');
  const tailLength = document.getElementById('tailLength');
  const markings = document.getElementById('markingComplexity');
  // Additional markings
  const tpu = document.querySelector('#tpu');
  const squeaker = document.querySelector('#squeaker');
  const nfc = document.querySelector('#nfc');
  const horns = document.querySelector('#horns');
  const fan = document.querySelector('#fan');
  const jaw = document.querySelector('#jaw');

  serviceSelect.addEventListener('change', function(event) {
    if (serviceSelect.value !== '800') {
        // Show the follow-up question
        tailLengthWrapper.style.setProperty('display', 'block', 'important');
    } else {
        tailLengthWrapper.style.setProperty('display', 'none', 'important');
    }
  });

  function calculateQuote() {
    let total = 800;
    const basePrice = parseFloat(serviceSelect.value);
    const colors = parseFloat(colorsInput.value) || 0;
    const markingPrice = parseFloat(markings.value) || 0;
    let tailPrice = 0;
    if (serviceSelect.value !== '800' && tailLength) {
      tailPrice = parseFloat(tailLength.value) || 0;
    }
    const colorRate = 50; // Set $/yard for each color
    if (colors > 3) {
        total = basePrice + tailPrice + markingPrice + ((colors-3.0) * colorRate);
    } else {
        total = basePrice + tailPrice + markingPrice;
    }
    if (tpu.checked) total = total + 40.00;
    if (squeaker.checked) total = total + 20.00;
    if (nfc.checked) total = total + 10.00;
    if (horns.checked) total = total + 100.00;
    if (fan.checked) total = total + 50.00;
    if (jaw.checked) total = total + 100.00;
    totalPriceDisplay.textContent = '$' + total.toFixed(2);
  }

  serviceSelect.addEventListener('change', calculateQuote);
  colorsInput.addEventListener('input', calculateQuote);
  tailLength.addEventListener('change', calculateQuote);
  markings.addEventListener('change', calculateQuote);
  tpu.addEventListener('click', calculateQuote);
  squeaker.addEventListener('click', calculateQuote);
  nfc.addEventListener('click', calculateQuote);
  horns.addEventListener('click', calculateQuote);
  fan.addEventListener('click', calculateQuote);
  jaw.addEventListener('click', calculateQuote);
</script>
