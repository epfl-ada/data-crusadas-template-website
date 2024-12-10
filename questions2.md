---
layout: default
title: Taste Preference Quiz
---

# Taste Preference Quiz

<div id="quiz-container" style="max-width: 600px; margin: auto; font-family: Arial, sans-serif;">
  <div id="question-container">
    <!-- Questions will be displayed here dynamically -->
  </div>
  <div id="navigation-buttons" style="text-align: center; margin-top: 20px;">
    <button id="prev-button" style="display: none;" onclick="prevQuestion()">Previous</button>
    <button id="next-button" onclick="nextQuestion()">Next</button>
  </div>
</div>

<!-- Result Display -->
<div id="result-container" style="display: none; text-align: center; margin-top: 40px;">
  <h2>Your Results</h2>
  <p id="result-text"></p>
  <a id="result-link" href="#" style="display: block; margin-top: 20px;">See Your Recommendation</a>
</div>

<script>
  const questions = [
    { id: "pc1", text: "Balanced vs. Rare Specialty", options: ["Balanced", "Rare specialty"] },
    { id: "pc2", text: "Dark/Roasty vs. Light/Hoppy", options: ["Dark/Roasty", "Light/Hoppy"] },
    { id: "pc3", text: "Bitter/Hoppy vs. Sour/Fruity", options: ["Bitter/Hoppy", "Sour/Fruity"] },
    { id: "pc4", text: "Complex/Citrusy vs. Simple/Grainy", options: ["Complex/Citrusy", "Simple/Grainy"] },
    { id: "pc5", text: "Wheat/Coffee vs. Malt-heavy/Sweet", options: ["Wheat/Coffee", "Malt-heavy/Sweet"] },
    { id: "pc6", text: "Barrel/Vanilla vs. Spicy/Pumpkin", options: ["Barrel/Vanilla", "Spicy/Pumpkin"] },
    { id: "pc7", text: "Tart/Funky Sour vs. Spicy/Wheat Belgian", options: ["Tart/Funky Sour", "Spicy/Wheat Belgian"] },
    { id: "pc8", text: "Nuanced Aroma vs. Straightforward Flavors", options: ["Nuanced Aroma", "Straightforward Flavors"] }
  ];

  let currentQuestion = 0;
  const responses = {};

  function renderQuestion() {
    const container = document.getElementById("question-container");
    container.innerHTML = ""; // Clear current content

    const question = questions[currentQuestion];
    const questionHtml = `
      <h3 style="text-align: center;">Question ${currentQuestion + 1} of ${questions.length}</h3>
      <p style="font-size: 18px; text-align: center;">${question.text}</p>
      <div style="display: flex; justify-content: center; margin-top: 20px;">
        ${question.options
          .map(
            (option) => `
          <label style="margin-right: 20px;">
            <input type="radio" name="${question.id}" value="${option}" ${
              responses[question.id] === option ? "checked" : ""
            } required> ${option}
          </label>
        `
          )
          .join("")}
      </div>
    `;
    container.innerHTML = questionHtml;

    // Update navigation button visibility
    document.getElementById("prev-button").style.display = currentQuestion > 0 ? "inline-block" : "none";
    document.getElementById("next-button").innerText =
      currentQuestion === questions.length - 1 ? "Submit" : "Next";
  }

  function nextQuestion() {
    const question = questions[currentQuestion];
    const selectedOption = document.querySelector(`input[name="${question.id}"]:checked`);

    if (!selectedOption) {
      alert("Please select an option before proceeding.");
      return;
    }

    // Save the response
    responses[question.id] = selectedOption.value;

    if (currentQuestion < questions.length - 1) {
      currentQuestion++;
      renderQuestion();
    } else {
      showResults();
    }
  }

  function prevQuestion() {
    if (currentQuestion > 0) {
      currentQuestion--;
      renderQuestion();
    }
  }

  function showResults() {
    // Hide quiz container
    document.getElementById("quiz-container").style.display = "none";

    // Show results
    const resultContainer = document.getElementById("result-container");
    resultContainer.style.display = "block";

    // Compute a result page path based on responses (example logic)
    const pathCode = `${responses.pc1}-${responses.pc2}`;
    let resultPage;
    switch (pathCode) {
      case "Balanced-Dark/Roasty": resultPage = "result1.html"; break;
      case "Balanced-Light/Hoppy": resultPage = "result2.html"; break;
      case "Rare specialty-Dark/Roasty": resultPage = "result3.html"; break;
      case "Rare specialty-Light/Hoppy": resultPage = "result4.html"; break;
      default: resultPage = "result-default.html"; break;
    }

    // Display result
    document.getElementById("result-text").innerText = "Thank you for completing the quiz!";
    const resultLink = document.getElementById("result-link");
    resultLink.href = `/${resultPage}`;
    resultLink.innerText = "See Your Recommendation";
  }

  // Initialize the quiz
  renderQuestion();
</script>
