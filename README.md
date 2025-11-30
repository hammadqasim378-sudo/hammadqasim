
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Modern Calculator Hub</title>
    <!-- Load Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Configure Tailwind for a sleek, modern look -->
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        'primary': '#10b981', // Emerald Green
                        'secondary': '#0f172a', // Slate Blue/Dark Background
                        'tertiary': '#334155', // Slate Gray
                    },
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <style>
        /* Custom styles for the calculator grid and typography */
        body {
            font-family: 'Inter', sans-serif;
            background-color: #0f172a; /* Secondary color for dark mode */
        }
        .calc-button {
            transition: all 0.1s ease-in-out;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.2), 0 2px 4px -2px rgba(0, 0, 0, 0.1);
        }
        .calc-button:active {
            transform: translateY(1px);
            box-shadow: none;
        }
        /* Style for the display font */
        .calc-display {
            font-size: 2.5rem; /* Larger font for modern feel */
            min-height: 80px;
            word-break: break-all;
        }

        /* Style for the secondary function buttons (operators) */
        .operator-button {
            background-color: #059669; /* Darker emerald for contrast */
            color: #d1fae5;
        }
        .operator-button:hover {
            background-color: #047857;
        }

        /* Style for the primary buttons (numbers) */
        .number-button {
            background-color: #334155; /* Tertiary/slate color */
            color: white;
        }
        .number-button:hover {
            background-color: #475569;
        }

        /* Style for the AC/DEL buttons */
        .utility-button {
            background-color: #ef4444; /* Red for clear/delete */
            color: white;
        }
        .utility-button:hover {
            background-color: #dc2626;
        }

        /* Style for the Equals button */
        .equals-button {
            background-color: #10b981; /* Primary emerald */
            color: #0f172a; /* Dark text for contrast */
            font-weight: bold;
        }
        .equals-button:hover {
            background-color: #059669;
        }

        /* AdSense Placeholder Styling */
        .adsense-placeholder {
            min-height: 90px;
            background-color: rgba(255, 255, 255, 0.05);
            border: 2px dashed #374151;
            color: #9ca3af;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            font-size: 0.875rem;
            margin-bottom: 1.5rem;
            border-radius: 0.5rem;
        }

        /* Style for the date input to match dark theme */
        input[type="date"] {
            color-scheme: dark;
        }
    </style>
</head>
<body class="min-h-screen text-white">

    <div class="container mx-auto p-4 max-w-7xl">
        <!-- Header and Navigation -->
        <header class="flex flex-col md:flex-row justify-between items-center py-6 border-b border-primary/30 mb-8">
            <h1 class="text-4xl font-extrabold text-primary mb-4 md:mb-0">
                Modern Calculator Hub
            </h1>
            <nav class="flex space-x-4">
                <button id="nav-calculators" onclick="switchView('calculators')" class="px-4 py-2 rounded-full font-medium transition duration-300 hover:bg-primary/20 bg-primary text-secondary">
                    Calculators
                </button>
                <button id="nav-articles" onclick="switchView('articles')" class="px-4 py-2 rounded-full font-medium transition duration-300 hover:bg-primary/20 bg-tertiary hover:bg-tertiary/80">
                    Articles
                </button>
            </nav>
        </header>

        <!-- Main Content Area -->
        <main class="grid grid-cols-1 lg:grid-cols-3 gap-8">
            <!-- Left/Center Column: Calculators/Articles View -->
            <div id="main-content-view" class="lg:col-span-2">
                
                <!-- AdSense Placeholder 1 (Top Banner) -->
                <div class="adsense-placeholder mb-6 h-24">
                    [ Google AdSense: Leaderboard Banner (728x90) ]
                </div>

                <!-- Calculators View -->
                <section id="calculators-view" class="view-section">
                    <h2 class="text-3xl font-bold mb-6 text-white">Online Calculator Tools</h2>

                    <!-- Calculator Selector / Tabs -->
                    <div class="flex space-x-3 mb-6 p-2 bg-tertiary/50 rounded-lg shadow-xl overflow-x-auto">
                        <button onclick="switchCalculator('basic')" class="calc-type-button px-4 py-2 rounded-lg text-sm font-semibold transition duration-150 bg-primary text-secondary" data-calc="basic">Basic</button>
                        <button onclick="switchCalculator('scientific')" class="calc-type-button px-4 py-2 rounded-lg text-sm font-semibold transition duration-150 hover:bg-primary/50 bg-tertiary" data-calc="scientific">Scientific</button>
                        <button onclick="switchCalculator('age')" class="calc-type-button px-4 py-2 rounded-lg text-sm font-semibold transition duration-150 hover:bg-primary/50 bg-tertiary" data-calc="age">Age</button>
                        <button onclick="switchCalculator('bmi')" class="calc-type-button px-4 py-2 rounded-lg text-sm font-semibold transition duration-150 hover:bg-primary/50 bg-tertiary" data-calc="bmi">BMI</button>
                    </div>

                    <!-- Calculator Interface Container -->
                    <div id="calculator-interface-container" class="bg-secondary/70 p-6 rounded-2xl shadow-2xl">
                        
                        <!-- 1. Basic/Scientific Calculator UI (Default) -->
                        <div id="basic-scientific-calc" class="calculator-ui active-calc-ui">
                            <!-- Display -->
                            <div class="bg-tertiary/70 mb-4 p-4 rounded-xl text-right overflow-hidden shadow-inner">
                                <div id="display-history" class="text-sm text-gray-400 h-6"></div>
                                <div id="display-output" class="calc-display font-light text-white overflow-x-scroll">0</div>
                            </div>
                            
                            <!-- Buttons Grid -->
                            <div id="calculator-grid" class="grid grid-cols-4 gap-3">
                                <!-- Scientific Row (Hidden by default) -->
                                <button data-op="sin" class="scientific-btn operator-button rounded-xl p-4 text-xl hidden">sin</button>
                                <button data-op="cos" class="scientific-btn operator-button rounded-xl p-4 text-xl hidden">cos</button>
                                <button data-op="log" class="scientific-btn operator-button rounded-xl p-4 text-xl hidden">log</button>
                                <button data-op="exp" class="scientific-btn operator-button rounded-xl p-4 text-xl hidden">^</button>

                                <!-- Row 1 -->
                                <button data-op="AC" class="col-span-2 utility-button rounded-xl p-4 text-2xl calc-button">AC</button>
                                <button data-op="DEL" class="utility-button rounded-xl p-4 text-2xl calc-button">DEL</button>
                                <button data-op="/" class="operator-button rounded-xl p-4 text-2xl calc-button">/</button>
                                
                                <!-- Row 2 -->
                                <button data-num="7" class="number-button rounded-xl p-4 text-2xl calc-button">7</button>
                                <button data-num="8" class="number-button rounded-xl p-4 text-2xl calc-button">8</button>
                                <button data-num="9" class="number-button rounded-xl p-4 text-2xl calc-button">9</button>
                                <button data-op="*" class="operator-button rounded-xl p-4 text-2xl calc-button">×</button>
                                
                                <!-- Row 3 -->
                                <button data-num="4" class="number-button rounded-xl p-4 text-2xl calc-button">4</button>
                                <button data-num="5" class="number-button rounded-xl p-4 text-2xl calc-button">5</button>
                                <button data-num="6" class="number-button rounded-xl p-4 text-2xl calc-button">6</button>
                                <button data-op="-" class="operator-button rounded-xl p-4 text-2xl calc-button">-</button>
                                
                                <!-- Row 4 -->
                                <button data-num="1" class="number-button rounded-xl p-4 text-2xl calc-button">1</button>
                                <button data-num="2" class="number-button rounded-xl p-4 text-2xl calc-button">2</button>
                                <button data-num="3" class="number-button rounded-xl p-4 text-2xl calc-button">3</button>
                                <button data-op="+" class="operator-button rounded-xl p-4 text-2xl calc-button">+</button>
                                
                                <!-- Row 5 -->
                                <button data-op="neg" class="number-button rounded-xl p-4 text-2xl calc-button">±</button>
                                <button data-num="0" class="number-button rounded-xl p-4 text-2xl calc-button">0</button>
                                <button data-num="." class="number-button rounded-xl p-4 text-2xl calc-button">.</button>
                                <button data-op="=" class="equals-button rounded-xl p-4 text-2xl calc-button">=</button>
                            </div>
                        </div>

                        <!-- 2. BMI Calculator UI -->
                        <div id="bmi-calc-ui" class="calculator-ui hidden">
                            <h3 class="text-2xl font-semibold text-primary mb-4">Body Mass Index (BMI) Calculator</h3>
                            <div class="space-y-4">
                                <div>
                                    <label for="bmi-weight" class="block text-sm font-medium text-gray-300">Weight (kg)</label>
                                    <input type="number" id="bmi-weight" placeholder="Enter weight in kilograms" class="mt-1 block w-full rounded-lg bg-tertiary/50 border-gray-600 p-3 text-white focus:ring-primary focus:border-primary">
                                </div>
                                <div>
                                    <label for="bmi-height" class="block text-sm font-medium text-gray-300">Height (cm)</label>
                                    <input type="number" id="bmi-height" placeholder="Enter height in centimeters" class="mt-1 block w-full rounded-lg bg-tertiary/50 border-gray-600 p-3 text-white focus:ring-primary focus:border-primary">
                                </div>
                                <button onclick="calculateBMI()" class="w-full equals-button rounded-xl p-3 text-lg calc-button mt-6">Calculate BMI</button>
                            </div>
                            <div id="bmi-result" class="mt-6 p-4 rounded-xl bg-tertiary/70 border border-primary/50 hidden">
                                <p class="font-semibold text-lg text-primary">Result:</p>
                                <p id="bmi-value" class="text-3xl font-bold"></p>
                                <p id="bmi-category" class="text-xl"></p>
                            </div>
                        </div>

                        <!-- 3. Age Calculator UI (New Feature) -->
                        <div id="age-calc-ui" class="calculator-ui hidden">
                            <h3 class="text-2xl font-semibold text-primary mb-4">Age Calculator</h3>
                            <div class="space-y-4">
                                <div>
                                    <label for="age-dob" class="block text-sm font-medium text-gray-300">Date of Birth</label>
                                    <input type="date" id="age-dob" class="mt-1 block w-full rounded-lg bg-tertiary/50 border-gray-600 p-3 text-white focus:ring-primary focus:border-primary">
                                </div>
                                <button onclick="calculateAge()" class="w-full equals-button rounded-xl p-3 text-lg calc-button mt-6">Calculate Age</button>
                            </div>
                            <div id="age-result" class="mt-6 p-4 rounded-xl bg-tertiary/70 border border-primary/50 hidden">
                                <p class="font-semibold text-lg text-primary">Your Age:</p>
                                <p id="age-value" class="text-3xl font-bold text-white"></p>
                                <p id="age-breakdown" class="text-sm text-gray-400 mt-2"></p>
                            </div>
                        </div>
                    </div>
                </section>

                <!-- Articles View (Initially Hidden) -->
                <section id="articles-view" class="view-section hidden mt-10">
                    <h2 class="text-3xl font-bold mb-6 text-white">Latest Articles & Tips</h2>
                    <div class="space-y-6">
                        <!-- Mock Article 1 -->
                        <article class="bg-tertiary/50 p-6 rounded-xl shadow-lg hover:shadow-primary/20 transition duration-300">
                            <h3 class="text-2xl font-semibold text-primary mb-2">Mastering the Order of Operations: PEMDAS</h3>
                            <p class="text-gray-300 mb-3">Learn the essential rules of arithmetic (Parentheses, Exponents, Multiplication, Division, Addition, Subtraction) to ensure flawless calculator results every time. Why $2+2 \times 2$ isn't $8$.</p>
                            <a href="#" class="text-sm text-primary hover:text-white font-medium">Read More &rarr;</a>
                        </article>

                        <!-- Mock Article 2 -->
                        <article class="bg-tertiary/50 p-6 rounded-xl shadow-lg hover:shadow-primary/20 transition duration-300">
                            <h3 class="2xl font-semibold text-primary mb-2">The Secret to Quick Loan Amortization Calculations</h3>
                            <p class="text-gray-300 mb-3">A deep dive into how financial calculators determine your monthly mortgage or loan payments, and the key formulas you need to understand your budget.</p>
                            <a href="#" class="text-sm text-primary hover:text-white font-medium">Read More &rarr;</a>
                        </article>

                        <!-- Mock Article 3 -->
                        <article class="bg-tertiary/50 p-6 rounded-xl shadow-lg hover:shadow-primary/20 transition duration-300">
                            <h3 class="2xl font-semibold text-primary mb-2">Graphing Trigonometry: Visualizing Sine and Cosine</h3>
                            <p class="text-gray-300 mb-3">An introduction to plotting trigonometric functions and how a graphing calculator can help you visualize wave patterns in physics and engineering.</p>
                            <a href="#" class="text-sm text-primary hover:text-white font-medium">Read More &rarr;</a>
                        </article>
                    </div>
                </section>
            </div>

            <!-- Right Column: Sidebar for Ads and Utilities -->
            <aside class="lg:col-span-1">
                <!-- AdSense Placeholder 2 (Sidebar Ad) -->
                <div class="adsense-placeholder h-72">
                    [ Google AdSense: Vertical Rectangle (300x600) ]
                </div>
                
                <!-- Utility Panel -->
                <div class="bg-tertiary/50 p-6 rounded-2xl shadow-xl mt-8">
                    <h3 class="text-xl font-bold text-primary mb-4">Quick Links</h3>
                    <ul class="space-y-3">
                        <li><a href="#" class="text-gray-300 hover:text-primary transition">Unit Converter</a></li>
                        <li><a href="#" class="text-gray-300 hover:text-primary transition">Currency Exchange Rates</a></li>
                        <li><a href="#" class="text-gray-300 hover:text-primary transition">Privacy Policy</a></li>
                    </ul>
                </div>
            </aside>
        </main>

        <!-- Footer -->
        <footer class="mt-12 pt-6 border-t border-primary/30 text-center text-gray-500">
            &copy; 2025 Modern Calculator Hub. All rights reserved.
        </footer>
    </div>

    <script>
        // =======================================================================
        // APP VIEW AND CALCULATOR SWITCHING LOGIC
        // =======================================================================

        let currentView = 'calculators';
        let currentCalculator = 'basic';

        function switchView(viewName) {
            currentView = viewName;
            
            document.querySelectorAll('.view-section').forEach(section => {
                section.classList.add('hidden');
            });
            document.getElementById(`${viewName}-view`).classList.remove('hidden');

            // Update navigation button styles
            document.getElementById('nav-calculators').classList.remove('bg-primary', 'text-secondary', 'bg-tertiary', 'hover:bg-tertiary/80');
            document.getElementById('nav-articles').classList.remove('bg-primary', 'text-secondary', 'bg-tertiary', 'hover:bg-tertiary/80');

            if (viewName === 'calculators') {
                document.getElementById('nav-calculators').classList.add('bg-primary', 'text-secondary');
                document.getElementById('nav-articles').classList.add('bg-tertiary', 'hover:bg-tertiary/80');
            } else {
                document.getElementById('nav-articles').classList.add('bg-primary', 'text-secondary');
                document.getElementById('nav-calculators').classList.add('bg-tertiary', 'hover:bg-tertiary/80');
            }
        }

        function switchCalculator(calcName) {
            currentCalculator = calcName;

            // Hide all calculator UIs
            document.querySelectorAll('.calculator-ui').forEach(ui => {
                ui.classList.add('hidden');
            });

            // Show the selected calculator UI
            if (calcName === 'basic' || calcName === 'scientific') {
                document.getElementById('basic-scientific-calc').classList.remove('hidden');
            } else {
                // This handles 'bmi' and the new 'age' calculator
                document.getElementById(`${calcName}-calc-ui`).classList.remove('hidden');
            }
            
            // Toggle Scientific Buttons Visibility
            const scientificBtns = document.querySelectorAll('.scientific-btn');
            if (calcName === 'scientific') {
                scientificBtns.forEach(btn => btn.classList.remove('hidden'));
                document.getElementById('calculator-grid').style.gridTemplateRows = 'repeat(6, minmax(0, 1fr))';
            } else {
                scientificBtns.forEach(btn => btn.classList.add('hidden'));
                document.getElementById('calculator-grid').style.gridTemplateRows = 'repeat(5, minmax(0, 1fr))';
            }

            // Update tab styles
            document.querySelectorAll('.calc-type-button').forEach(btn => {
                btn.classList.remove('bg-primary', 'text-secondary');
                btn.classList.add('bg-tertiary', 'hover:bg-primary/50');
                if (btn.getAttribute('data-calc') === calcName) {
                    btn.classList.add('bg-primary', 'text-secondary');
                    btn.classList.remove('bg-tertiary', 'hover:bg-primary/50');
                }
            });

            // Reset basic/scientific calculator state when switching modes away from basic/scientific
            if (calcName === 'bmi' || calcName === 'age') {
                // Do nothing
            } else {
                resetCalculator();
            }
        }
        
        // =======================================================================
        // BASIC / SCIENTIFIC CALCULATOR LOGIC
        // =======================================================================

        const displayOutput = document.getElementById('display-output');
        const displayHistory = document.getElementById('display-history');
        const buttons = document.querySelectorAll('#calculator-grid button');

        let currentInput = '0';
        let previousInput = '';
        let operation = null;
        let waitingForSecondOperand = false;

        function updateDisplay() {
            displayOutput.textContent = currentInput.slice(0, 16); // Limit display length
            displayHistory.textContent = previousInput + (operation ? ' ' + operation : '');
        }

        function clearAll() {
            currentInput = '0';
            previousInput = '';
            operation = null;
            waitingForSecondOperand = false;
        }

        function deleteLast() {
            if (currentInput === '0' || currentInput === 'Error') return;
            currentInput = currentInput.slice(0, -1);
            if (currentInput === '' || currentInput === '-') {
                currentInput = '0';
            }
        }

        function inputNumber(number) {
            if (currentInput === 'Error') {
                clearAll();
            }
            
            if (waitingForSecondOperand) {
                currentInput = number;
                waitingForSecondOperand = false;
            } else {
                if (currentInput.length >= 16) return; // Prevent overflow
                currentInput = currentInput === '0' ? number : currentInput + number;
            }
        }

        function inputDecimal() {
            if (waitingForSecondOperand) {
                currentInput = '0.';
                waitingForSecondOperand = false;
                return;
            }
            if (!currentInput.includes('.')) {
                currentInput += '.';
            }
        }

        function toggleNegative() {
            if (currentInput.startsWith('-')) {
                currentInput = currentInput.substring(1);
            } else if (currentInput !== '0' && currentInput !== 'Error') {
                currentInput = '-' + currentInput;
            }
        }

        function performScientificOperation(op) {
            if (currentInput === 'Error') return;
            const value = parseFloat(currentInput);
            let result;

            try {
                switch (op) {
                    case 'sin':
                        result = Math.sin(value * (Math.PI / 180)); // Assume degrees
                        break;
                    case 'cos':
                        result = Math.cos(value * (Math.PI / 180)); // Assume degrees
                        break;
                    case 'log':
                        if (value <= 0) throw new Error("Log Error");
                        result = Math.log10(value);
                        break;
                    case 'exp':
                        // This will be handled as a binary operation, waiting for the power
                        operation = '^';
                        previousInput = currentInput;
                        waitingForSecondOperand = true;
                        updateDisplay();
                        return;
                    default:
                        return;
                }
                currentInput = result.toPrecision(10).replace(/\.?0+$/, "");
            } catch (e) {
                currentInput = 'Error';
            }
            operation = null;
            previousInput = '';
        }

        function handleOperator(nextOperation) {
            if (currentInput === 'Error') return;
            const inputValue = parseFloat(currentInput);

            if (previousInput === '') {
                previousInput = currentInput;
            } else if (!waitingForSecondOperand) {
                const prevValue = parseFloat(previousInput);
                let result;

                // Simple Calculation Logic
                try {
                    switch (operation) {
                        case '+':
                            result = prevValue + inputValue;
                            break;
                        case '-':
                            result = prevValue - inputValue;
                            break;
                        case '*':
                            result = prevValue * inputValue;
                            break;
                        case '/':
                            if (inputValue === 0) throw new Error("Division by zero");
                            result = prevValue / inputValue;
                            break;
                        case '^':
                            result = Math.pow(prevValue, inputValue);
                            break;
                        default:
                            return;
                    }
                    // Format result (limit to 10 significant digits)
                    currentInput = result.toPrecision(10).replace(/\.?0+$/, "");
                    previousInput = currentInput;
                } catch (e) {
                    currentInput = 'Error';
                    previousInput = '';
                    operation = null;
                    updateDisplay();
                    return;
                }
            }

            if (nextOperation === '=') {
                operation = null;
                previousInput = '';
            } else {
                operation = nextOperation;
                waitingForSecondOperand = true;
            }
        }

        buttons.forEach(button => {
            button.addEventListener('click', () => {
                const num = button.getAttribute('data-num');
                const op = button.getAttribute('data-op');

                if (num) {
                    if (num === '.') {
                        inputDecimal();
                    } else {
                        inputNumber(num);
                    }
                } else if (op) {
                    if (op === 'AC') {
                        clearAll();
                    } else if (op === 'DEL') {
                        deleteLast();
                    } else if (op === 'neg') {
                        toggleNegative();
                    } else if (['sin', 'cos', 'log', 'exp'].includes(op) && currentCalculator === 'scientific') {
                         performScientificOperation(op);
                    } else if (['+', '-', '*', '/', '^', '='].includes(op)) {
                        if (op === '^' && currentCalculator !== 'scientific') return;
                        handleOperator(op);
                    }
                }
                updateDisplay();
            });
        });

        function resetCalculator() {
            clearAll();
            updateDisplay();
        }

        // =======================================================================
        // BMI CALCULATOR LOGIC
        // =======================================================================
        
        function calculateBMI() {
            const weightKg = parseFloat(document.getElementById('bmi-weight').value);
            const heightCm = parseFloat(document.getElementById('bmi-height').value);
            const resultDiv = document.getElementById('bmi-result');
            const valueP = document.getElementById('bmi-value');
            const categoryP = document.getElementById('bmi-category');

            resultDiv.classList.add('hidden');
            valueP.textContent = '';
            categoryP.textContent = '';
            categoryP.className = 'text-xl'; // Reset classes

            if (isNaN(weightKg) || isNaN(heightCm) || weightKg <= 0 || heightCm <= 0) {
                alertUser("Please enter valid positive numbers for both weight and height.", "error");
                return;
            }

            // Convert height from cm to meters
            const heightM = heightCm / 100;
            // BMI Formula: weight (kg) / [height (m)]^2
            const bmi = weightKg / (heightM * heightM);
            const roundedBmi = bmi.toFixed(1);

            let category = '';
            let colorClass = 'text-white';

            if (bmi < 18.5) {
                category = 'Underweight';
                colorClass = 'text-blue-400';
            } else if (bmi >= 18.5 && bmi < 25) {
                category = 'Normal Weight';
                colorClass = 'text-green-400';
            } else if (bmi >= 25 && bmi < 30) {
                category = 'Overweight';
                colorClass = 'text-yellow-400';
            } else {
                category = 'Obese';
                colorClass = 'text-red-500';
            }

            valueP.textContent = roundedBmi;
            categoryP.textContent = category;
            categoryP.classList.add(colorClass);
            resultDiv.classList.remove('hidden');
        }

        // =======================================================================
        // AGE CALCULATOR LOGIC (New)
        // =======================================================================
        
        function calculateAge() {
            const dobInput = document.getElementById('age-dob');
            const dobValue = dobInput.value;
            const resultDiv = document.getElementById('age-result');
            const ageValueP = document.getElementById('age-value');
            const ageBreakdownP = document.getElementById('age-breakdown');

            resultDiv.classList.add('hidden');
            ageValueP.textContent = '';
            ageBreakdownP.textContent = '';

            if (!dobValue) {
                alertUser("Please select your date of birth.", "error");
                return;
            }

            const dob = new Date(dobValue);
            const today = new Date();
            
            // Check if DOB is in the future
            if (dob > today) {
                alertUser("Date of birth cannot be in the future.", "error");
                return;
            }

            // Calculate age components
            let years = today.getFullYear() - dob.getFullYear();
            let months = today.getMonth() - dob.getMonth();
            let days = today.getDate() - dob.getDate();

            // Adjust days if negative
            if (days < 0) {
                months--;
                // Get the number of days in the previous month (month index is 0-based)
                // Passing 0 as the day returns the last day of the previous month
                const prevMonth = new Date(today.getFullYear(), today.getMonth(), 0);
                days += prevMonth.getDate();
            }

            // Adjust months if negative
            if (months < 0) {
                years--;
                months += 12;
            }
            
            // Output formatting
            ageValueP.textContent = `${years} years old`;
            ageBreakdownP.textContent = `Total breakdown: ${years} years, ${months} months, and ${days} days.`;
            
            resultDiv.classList.remove('hidden');
        }

        // =======================================================================
        // INITIALIZATION
        // =======================================================================

        // Initial setup for the Basic Calculator and View
        window.onload = () => {
            switchView('calculators');
            switchCalculator('basic');
        };

        // Custom alert function (since native alert() is forbidden)
        function alertUser(message, type) {
            // For this single-file demo, we temporarily show a message on the calculator display
            console.warn(`[${type.toUpperCase()} Notification]: ${message}`);
            
            if (type === 'error' && currentCalculator !== 'basic' && currentCalculator !== 'scientific') {
                 // For non-basic calculators, use a simple prompt display or console log
                 const container = document.getElementById(`${currentCalculator}-calc-ui`);
                 const existingError = container.querySelector('.temp-error-message');
                 if (existingError) existingError.remove();

                 const errorMessage = document.createElement('div');
                 errorMessage.className = 'temp-error-message text-red-400 p-2 mt-4 rounded-lg bg-red-900/50';
                 errorMessage.textContent = message;
                 container.appendChild(errorMessage);

                 setTimeout(() => {
                    errorMessage.remove();
                 }, 4000); // Remove after 4 seconds

            } else if (type === 'error') {
                 // For basic/scientific calculator
                 displayOutput.textContent = 'Error: ' + message.split(':')[0];
            }
        }
    </script>
</body>
</html>
