<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Symptom Checker</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f4;
      text-align: center;
      padding: 20px;
    }
    .container {
      background: white;
      max-width: 400px;
      margin: auto;
      padding: 20px;
      box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.1);
      border-radius: 8px;
      margin-bottom: 20px;
    }
    input, button {
      padding: 10px;
      margin: 5px;
      width: 90%;
    }
    button {
      background-color: #28a745;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    button:hover {
      background-color: #218838;
    }
  </style>
</head>
<body>

  <!-- Registration Form -->
  <div class="container" id="registrationForm">
    <h2>Registration</h2>
    <input type="text" id="name" placeholder="Enter your name" required /><br>
    <input type="number" id="age" placeholder="Enter your age" required /><br>
    <input type="email" id="email" placeholder="Enter your email" required /><br>
    <button onclick="saveRegistration()">Save &amp; Continue</button>
    <p id="saveMessage" style="display: none; color: green;">Registration saved!</p>
    <button id="startButton" onclick="startSymptomChecker()" style="display: none;">Start Symptom Checker</button>
  </div>

  <!-- Symptom Checker -->
  <div class="container" id="symptomChecker" style="display: none;">
    <h2>Symptom Checker</h2>
    <div id="question"></div>
  </div>

  <!-- Result Section -->
  <div class="container" id="result"></div>

  <script>
    let symptomsList = [
      { question: "Do you have a fever?", score: 2 },
      { question: "Do you have a cough?", score: 2 },
      { question: "Do you feel body pain?", score: 1 },
      { question: "Do you have a sore throat?", score: 1 },
      { question: "Have you lost your taste or smell?", score: 2 },
      { question: "Do you have difficulty breathing?", score: 3 },
      { question: "Are you feeling unusually tired?", score: 1 },
      { question: "Do you have a headache?", score: 1 },
      { question: "Are you experiencing chills?", score: 1 },
      { question: "Do you have nasal congestion?", score: 1 },
      { question: "Do you have diarrhea?", score: 1 },
      { question: "Are your eyes red or irritated?", score: 1 },
      { question: "Do you have joint pain?", score: 1 }
    ];

    let userSymptoms = [];
    let currentSymptomIndex = 0;
    let riskScore = 0;

    function saveRegistration() {
      let name = document.getElementById("name").value;
      let age = document.getElementById("age").value;
      let email = document.getElementById("email").value;

      if (name === "" || age === "" || email === "") {
        alert("Please fill out all fields!");
        return;
      }

      localStorage.setItem("name", name);
      localStorage.setItem("age", age);
      localStorage.setItem("email", email);

      document.getElementById("saveMessage").style.display = "block";
      document.getElementById("startButton").style.display = "block";
    }

    function startSymptomChecker() {
      document.getElementById("registrationForm").style.display = "none";
      document.getElementById("symptomChecker").style.display = "block";
      askNextSymptom();
    }

    function askNextSymptom() {
      if (currentSymptomIndex < symptomsList.length) {
        let questionText = symptomsList[currentSymptomIndex].question;
        document.getElementById("question").innerHTML = `
          <p>${questionText}</p>
          <button onclick="checkSymptom(true)">Yes</button>
          <button onclick="checkSymptom(false)">No</button>
        `;
      } else {
        showResult();
      }
    }

    function checkSymptom(hasSymptom) {
      if (hasSymptom) {
        userSymptoms.push(symptomsList[currentSymptomIndex].question);
        riskScore += symptomsList[currentSymptomIndex].score;
      }
      currentSymptomIndex++;
      askNextSymptom();
    }

    function showResult() {
      let resultMessage = "You seem fine! Stay hydrated and eat healthy.";
      let healthTips = "";
      let doctor = "No doctor needed";
      
      if (riskScore >= 8) {
        resultMessage = "You should consult a specialist immediately!";
        healthTips = "Take rest, stay hydrated, and monitor your symptoms closely.";
        doctor = "Dr. Smith (Pulmonologist - Lung Specialist)";
      } else if (riskScore >= 5) {
        resultMessage = "You may need to see a general physician.";
        healthTips = "Monitor your symptoms and take necessary precautions.";
        doctor = "Dr. Johnson (General Physician)";
      } else if (userSymptoms.includes("Do you have a fever?") && userSymptoms.includes("Do you have a cough?")) {
        resultMessage = "You may have the flu. Drink warm fluids and rest.";
        healthTips = "Try honey, ginger tea, and get plenty of sleep.";
        doctor = "Dr. Lee (Infectious Disease Specialist)";
      } else if (userSymptoms.includes("Do you have difficulty breathing?")) {
        resultMessage = "Seek medical attention immediately!";
        healthTips = "Call emergency services and avoid physical exertion.";
        doctor = "Dr. Brown (Emergency Care Specialist)";
        alert("WARNING! Your symptoms indicate a serious condition. Seek medical help now!");
      }

      document.getElementById("question").innerHTML = "";
      document.getElementById("result").innerHTML = `
        <h3>Diagnosis Result</h3>
        <p>${resultMessage}</p>
        <p><strong>Health Tips:</strong> ${healthTips}</p>
        <p><strong>Risk Score:</strong> ${riskScore}/10</p>
        <p><strong>Recommended Doctor:</strong> ${doctor}</p>
      `;
    }
  </script>

</body>
</html>
