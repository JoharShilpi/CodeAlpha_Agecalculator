<!DOCTYPE html>
<html lang="en">
<head>
    <title>Age Calculator</title>
    <style>
        :root {
   --primary-color: #4361ee;
   --secondary-color: #3f37c9;
   --accent-color: #4895ef;
   --light-color: #f8f9fa;
   --dark-color: #212529;
   --success-color: #4cc9f0;
   --error-color: #f72585;
}

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: cursive;
}

body {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background: linear-gradient(135deg, #4203a9, #90bafc);
    padding: 20px;
}

.container {
    width: 100%;
    max-width: 500px;
    background-color: white;
    border-radius: 15px;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
    padding: 40px;
    animation: fadeIn 0.5s ease-in-out;}

@keyframes fadeIn {
    from { opacity: 0; transform: translateY(-20px); }
    to { opacity: 1; transform: translateY(0); }}

h1 {
    color: var(--dark-color);
    text-align: center;
    margin-bottom: 30px;
    font-size: 2.2rem;
    position: relative;}

h1::after {
    content: '';
    position: absolute;
    bottom: -10px;
    left: 50%;
    transform: translateX(-50%);
    width: 80px;
    height: 4px;
    background: var(--accent-color);
    border-radius: 2px;
}

.form-group {
    margin-bottom: 25px;
}

label {
    display: block;
    margin-bottom: 8px;
    color: var(--dark-color);
    font-weight: 600;
}

input[type="date"] {
     width: 100%;
    padding: 12px 15px;
    border: 2px solid #e9ecef;
    border-radius: 8px;
    font-size: 1rem;
    transition: all 0.3s ease;
}

input[type="date"]:focus {
    outline: none;
    border-color: var(--accent-color);
    box-shadow: 0 0 0 3px rgba(72, 149, 239, 0.25);
}

button {
     width: 100%;
    padding: 14px;
    background-color: var(--primary-color);
    color: white;
    border: none;
    border-radius: 8px;
    font-size: 1rem;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s ease;
    text-transform: uppercase;
    letter-spacing: 1px;
}

button:hover {
    background-color: var(--secondary-color);
    transform: translateY(-2px);
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
}

button:active {
    transform: translateY(0);
}

.result-container {
    margin-top: 30px;
    padding: 20px;
    background-color: #f8f9fa;
    border-radius: 10px;
    display: none;
    animation: fadeIn 0.5s ease-in-out;
}

.result-container.active {
    display: block;
}

.result-title {
    text-align: center;
    color: var(--dark-color);
    margin-bottom: 15px;
    font-size: 1.2rem;
}

.result-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
    gap: 15px;
}

.result-item {
    text-align: center;
    padding: 15px;
    background-color: white;
    border-radius: 8px;
    box-shadow: 0 3px 10px rgba(0, 0, 0, 0.05);
}

.result-value {
    font-size: 1.8rem;
    font-weight: 700;
    color: var(--primary-color);
    margin-bottom: 5px;
}

.result-label {
    font-size: 0.9rem;
    color: #6c757d;
}

footer {
    margin-top: 30px;
    text-align: center;
    color: #6c757d;
    font-size: 0.9rem;
}

@media (max-width: 600px) {
    .container {
        padding: 30px 20px;
    }
            
h1 {
    font-size: 1.8rem;
}
            
.result-grid {
    grid-template-columns: 1fr;
}
}
</style>
</head>
<body>
    <div class="container">
        <h1>Age Calculator</h1>
        
        <div class="form-group">
            <label for="dob">Enter Your Date of Birth</label>
            <input type="date" id="dob" name="dob">
        </div>
        
        <button id="calculate-btn">Calculate Age</button>
        
        <div class="result-container" id="result-container">
            <h2 class="result-title">Your Age Details</h2>
            <div class="result-grid">
                <div class="result-item">
                    <div class="result-value" id="years">0</div>
                    <div class="result-label">Years</div>
                </div>
                <div class="result-item">
                    <div class="result-value" id="months">0</div>
                    <div class="result-label">Months</div>
                </div>
                <div class="result-item">
                    <div class="result-value" id="days">0</div>
                    <div class="result-label">Days</div>
                </div>
                <div class="result-item">
                    <div class="result-value" id="hours">0</div>
                    <div class="result-label">Hours</div>
                </div>
            </div>
        </div>
    </div>
    
    <footer>
        <p>© <span id="current-year"></span> Age Calculator | All Rights Reserved</p>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
    const today = new Date().toISOString().split('T')[0];
    document.getElementById('dob').setAttribute('max', today);
            
    document.getElementById('current-year').textContent = new Date().getFullYear();
            
    document.getElementById('calculate-btn').addEventListener('click', calculateAge);
});
        
function calculateAge() {
    const dobInput = document.getElementById('dob');
    const resultContainer = document.getElementById('result-container');
        
    if (!dobInput.value) {
        alert('Please enter your date of birth');
        return;
    }
            
    const dob = new Date(dobInput.value);
    const referenceDate = new Date();
            
    if (dob > referenceDate) {
        alert('Date of birth cannot be in the future');
        return;
    }
            
    let years = referenceDate.getFullYear() - dob.getFullYear();
    let months = referenceDate.getMonth() - dob.getMonth();
    let days = referenceDate.getDate() - dob.getDate();
    let hours = referenceDate.getHours() - dob.getHours();
            
    if (months < 0 || (months === 0 && days < 0)) {
        years--;
        months += 12;
    }
            
    if (days < 0) {
        const lastMonth = new Date(
            referenceDate.getFullYear(), 
            referenceDate.getMonth(), 
            0
        );
        days = lastMonth.getDate() - dob.getDate() + referenceDate.getDate();
        months--;
    }
            
    if (hours < 0) {
        hours += 24;
        days--;
    }
            
    document.getElementById('years').textContent = years;
    document.getElementById('months').textContent = months;
    document.getElementById('days').textContent = days;
    document.getElementById('hours').textContent = hours;
        
    resultContainer.classList.add('active');
            
    resultContainer.scrollIntoView({ behavior: 'smooth' });
}
    </script>
</body>
</html>
