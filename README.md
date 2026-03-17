# Ex06 BMI Calculator
## Date: 17-03-2026

## AIM
To develop a responsive and interactive Body Mass Index (BMI) Calculator using React that allows users to input their height and weight, and calculates their BMI to categorize their health status (e.g., Underweight, Normal, Overweight, Obese).

## DESIGN STEPS

### STEP 1: Initialize React Project

<li>Create a new React app using create-react-app.</li>
<li>Install React Router using:</li>
npm install react-router-dom

### STEP 2: Set Up Routing

Create routing structure with react-router-dom:

<li>Home route (/) – Intro or Navigation</li>

<li>BMI Calculator route (/bmi)</li>

<li>Result route (/result)</li>

### STEP 3: Design the BMI Form Page

<li>Create a form to accept Height (in cm or m) and Weight (in kg).</li>

<li>On form submit, navigate to the result page with entered values via URL query params or context/state.</li>

## STEP 4: Handle Input Validation

<li>Check if height and weight are valid numbers.</li>

<li>Optionally, show error messages for invalid inputs.</li>

### STEP 5: Perform BMI Calculation

<li>In the result component:

<li>Extract height and weight from the route (URL or passed state).</li>

<li>Apply the BMI formula:</li>

![image](https://github.com/user-attachments/assets/ec785506-c96b-489e-8783-fb1a5d36101a)
​
 
<li>Convert height from cm to m if needed.</li></li>

### STEP 6: Display Result

<li>Show calculated BMI.</li>

<li>Show category based on BMI range:

<li>Underweight, Normal, Overweight, Obese, etc.</li></li>

### STEP 7: Navigation Options

<li>Provide a button to go back to the BMI form to calculate again.</li>

### STEP 8: Enhancements

<li>Add styling using CSS or Tailwind.</li>

## PROGRAM:
## app.css:
```css
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Roboto', sans-serif;
  background-color: #e0f7fa;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  color: #444;
}

.container {
  background-color: #ffffff;
  border-radius: 12px;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
  width: 100%;
  max-width: 420px;
  padding: 30px;
  text-align: center;
}

h1 {
  font-size: 28px;
  margin-bottom: 20px;
  color: #00796b;
  font-weight: 700;
}

.input-group {
  margin-bottom: 20px;
}

.input-group label {
  font-size: 18px;
  margin-bottom: 10px;
  color: #00796b;
}

.input-group input {
  width: 100%;
  padding: 12px;
  font-size: 18px;
  border: 2px solid #00796b;
  border-radius: 8px;
  background-color: #e0f7fa;
  color: #00796b;
  outline: none;
}

.input-group input:focus {
  border-color: #00054d;
  background-color: #ffffff;
}

.buttons {
  display: flex;
  justify-content: space-between;
  gap: 15px;
}

.btn {
  width: 48%;
  padding: 12px;
  font-size: 16px;
  font-weight: 600;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.calculate {
  background-color: #517900;
  color: white;
}

.calculate:hover {
  background-color: #414d00;
}

.reset {
  background-color: #f44336;
  color: white;
}

.reset:hover {
  background-color: #d32f2f;
}

.result {
  margin-top: 25px;
  padding: 15px;
  background-color: #f1f8e9;
  border-radius: 8px;
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.1);
}

h2 {
  font-size: 32px;
  color: #00796b;
  margin-bottom: 10px;
}

.category {
  font-size: 20px;
  font-weight: 600;
}

.underweight {
  color: #ffeb3b;
}

.normal-weight {
  color: #8e3838;
}

.overweight {
  color: #ff0066;
}

.obesity {
  color: #1923e6;
}
```
## app.jsx:
```jsx
import React, { useState } from "react";
import "./App.css";

function App() {
  const [weight, setWeight] = useState("");
  const [height, setHeight] = useState("");
  const [bmi, setBmi] = useState(null);
  const [category, setCategory] = useState("");

  const calculateBMI = () => {
    if (weight && height) {
      const heightInMeters = height / 100;
      const bmiValue = weight / (heightInMeters * heightInMeters);
      const bmiRounded = bmiValue.toFixed(2);

      setBmi(bmiRounded);

      if (bmiValue < 18.5) setCategory("Underweight");
      else if (bmiValue < 25) setCategory("Normal weight");
      else if (bmiValue < 30) setCategory("Overweight");
      else setCategory("Obesity");
    }
  };

  const reset = () => {
    setWeight("");
    setHeight("");
    setBmi(null);
    setCategory("");
  };

  return (
    <div className="container">
      <h1>BMI Calculator</h1>

      <div className="card">
        <div className="input-group">
          <label>Weight (kg):</label>
          <input
            type="number"
            value={weight}
            onChange={(e) => setWeight(e.target.value)}
          />
        </div>

        <div className="input-group">
          <label>Height (cm):</label>
          <input
            type="number"
            value={height}
            onChange={(e) => setHeight(e.target.value)}
          />
        </div>

        <div className="buttons">
          <button className="btn calculate" onClick={calculateBMI}>
            Calculate
          </button>

          <button className="btn reset" onClick={reset}>
            Reset
          </button>
        </div>

        {bmi && (
          <div className="result">
            <h2>Your BMI: {bmi}</h2>
            <p className={`category ${category.toLowerCase().replace(" ", "-")}`}>
              Category: {category}
            </p>
          </div>
        )}
      </div>

      <footer className="footer">
        
      </footer>
    </div>
  );
}

export default App;
```



## OUTPUT:
<img width="1916" height="1004" alt="image" src="https://github.com/user-attachments/assets/6982d678-734c-40e1-ad0c-dc9c34c8ac77" />
<img width="1917" height="870" alt="image" src="https://github.com/user-attachments/assets/0e8f6cc4-1715-4842-9577-648753bdd090" />






## RESULT
The BMI Calculator successfully takes user input for height and weight, performs the BMI calculation in real-time using React state and event handling, and displays the BMI value along with the corresponding health category.
