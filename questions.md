---
layout: default
title: Taste Preference Quiz
---

# Taste Preference Quiz

Please answer the following questions to find the best match for your preferences. Select one option for each question:

<form id="taste-quiz" onsubmit="handleSubmit(event)">
  <ol>
    <li>
      **Balanced vs. Rare Specialty (PC1):**  
      <label><input type="radio" name="pc1" value="balanced" required> Balanced</label>  
      <label><input type="radio" name="pc1" value="rare"> Rare specialty</label>
    </li>
    <li>
      **Dark/Roasty vs. Light/Hoppy (PC2):**  
      <label><input type="radio" name="pc2" value="dark"> Dark/Roasty</label>  
      <label><input type="radio" name="pc2" value="light"> Light/Hoppy</label>
    </li>
    <li>
      **Bitter/Hoppy vs. Sour/Fruity (PC3):**  
      <label><input type="radio" name="pc3" value="bitter"> Bitter/Hoppy</label>  
      <label><input type="radio" name="pc3" value="sour"> Sour/Fruity</label>
    </li>
    <li>
      **Complex/Citrusy vs. Simple/Grainy (PC4):**  
      <label><input type="radio" name="pc4" value="complex"> Complex/Citrusy</label>  
      <label><input type="radio" name="pc4" value="simple"> Simple/Grainy</label>
    </li>
    <li>
      **Wheat/Coffee vs. Malt-heavy/Sweet (PC5):**  
      <label><input type="radio" name="pc5" value="wheat"> Wheat/Coffee</label>  
      <label><input type="radio" name="pc5" value="malt"> Malt-heavy/Sweet</label>
    </li>
    <li>
      **Barrel/Vanilla vs. Spicy/Pumpkin (PC6):**  
      <label><input type="radio" name="pc6" value="barrel"> Barrel/Vanilla</label>  
      <label><input type="radio" name="pc6" value="spicy"> Spicy/Pumpkin</label>
    </li>
    <li>
      **Tart/Funky Sour vs. Spicy/Wheat Belgian (PC7):**  
      <label><input type="radio" name="pc7" value="tart"> Tart/Funky Sour</label>  
      <label><input type="radio" name="pc7" value="spicy"> Spicy/Wheat Belgian</label>
    </li>
    <li>
      **Nuanced Aroma vs. Straightforward Flavors (PC8):**  
      <label><input type="radio" name="pc8" value="nuanced"> Nuanced Aroma</label>  
      <label><input type="radio" name="pc8" value="straightforward"> Straightforward Flavors</label>
    </li>
  </ol>

  <button type="submit">See Results</button>
</form>

<script>
  function handleSubmit(event) {
    event.preventDefault();

    // Collect responses
    const form = document.forms["taste-quiz"];
    const responses = {
      pc1: form["pc1"].value,
      pc2: form["pc2"].value,
      pc3: form["pc3"].value,
      pc4: form["pc4"].value,
      pc5: form["pc5"].value,
      pc6: form["pc6"].value,
      pc7: form["pc7"].value,
      pc8: form["pc8"].value,
    };

    // Compute a result page path based on responses
    const resultPage = computeResultPath(responses);

    // Redirect to the result page
    window.location.href = `/${resultPage}`;
  }

  function computeResultPath(responses) {
    // Example logic: Combine responses to generate a path (can be customized)
    // For simplicity, this combines two answers as a "path code".
    const pathCode = `${responses.pc1}-${responses.pc2}`;
    switch (pathCode) {
      case "balanced-dark": return "result1.html";
      case "balanced-light": return "result2.html";
      case "rare-dark": return "result3.html";
      case "rare-light": return "result4.html";
      default: return "result-default.html"; // fallback
    }
  }
</script>
