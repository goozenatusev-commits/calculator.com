<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Красивый калькулятор</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background: linear-gradient(135deg, #6e8efb, #a777e3);
            padding: 20px;
        }
        
        .calculator-container {
            width: 100%;
            max-width: 400px;
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.2);
            overflow: hidden;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        
        .calculator-header {
            padding: 20px;
            background: rgba(0, 0, 0, 0.2);
            text-align: center;
            color: white;
        }
        
        .calculator-header h1 {
            font-size: 1.8rem;
            font-weight: 300;
            margin-bottom: 5px;
        }
        
        .calculator-header p {
            font-size: 0.9rem;
            opacity: 0.8;
        }
        
        .display {
            background: rgba(0, 0, 0, 0.4);
            color: white;
            text-align: right;
            padding: 30px 20px;
            font-size: 2.5rem;
            height: 120px;
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
            transition: all 0.3s ease;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .calculation-display {
            font-size: 1.2rem;
            color: rgba(255, 255, 255, 0.7);
            margin-bottom: 10px;
            min-height: 24px;
        }
        
        .buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 2px;
            background: rgba(0, 0, 0, 0.1);
            padding: 2px;
        }
        
        button {
            border: none;
            outline: none;
            background: rgba(255, 255, 255, 0.1);
            color: white;
            font-size: 1.5rem;
            padding: 20px;
            cursor: pointer;
            transition: all 0.2s ease;
            backdrop-filter: blur(5px);
        }
        
        button:hover {
            background: rgba(255, 255, 255, 0.2);
            transform: scale(1.02);
        }
        
        button:active {
            background: rgba(255, 255, 255, 0.3);
            transform: scale(0.98);
        }
        
        .operator {
            background: rgba(255, 149, 0, 0.3);
            font-weight: 500;
        }
        
        .operator:hover {
            background: rgba(255, 149, 0, 0.5);
        }
        
        .equals {
            background: linear-gradient(135deg, #6e8efb, #a777e3);
            font-weight: 600;
        }
        
        .equals:hover {
            background: linear-gradient(135deg, #7d9dfc, #b586f5);
        }
        
        .clear, .backspace {
            background: rgba(255, 87, 87, 0.3);
        }
        
        .clear:hover, .backspace:hover {
            background: rgba(255, 87, 87, 0.5);
        }
        
        .zero {
            grid-column: span 2;
            border-bottom-left-radius: 10px;
        }
        
        .equals {
            border-bottom-right-radius: 10px;
        }
        
        .memory-btn {
            font-size: 1.2rem;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .memory-indicator {
            position: absolute;
            top: 10px;
            right: 10px;
            color: white;
            font-size: 0.8rem;
            background: rgba(255, 255, 255, 0.2);
            padding: 5px 10px;
            border-radius: 10px;
            display: none;
        }
        
        .theme-toggle {
            position: absolute;
            top: 20px;
            right: 20px;
            background: rgba(255, 255, 255, 0.2);
            border: none;
            color: white;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .theme-toggle:hover {
            background: rgba(255, 255, 255, 0.3);
            transform: rotate(30deg);
        }
        
        @media (max-width: 480px) {
            button {
                padding: 16px;
                font-size: 1.3rem;
            }
            
            .display {
                padding: 25px 15px;
                font-size: 2rem;
                height: 100px;
            }
            
            .calculation-display {
                font-size: 1rem;
            }
        }
        
        /* Анимации */
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(-10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .calculator-container {
            animation: fadeIn 0.5s ease-out;
        }
        
        /* Светлая тема */
        .light-theme {
            background: linear-gradient(135deg, #f5f7fa, #c3cfe2);
        }
        
        .light-theme .calculator-container {
            background: rgba(255, 255, 255, 0.8);
            border: 1px solid rgba(255, 255, 255, 0.5);
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.1);
        }
        
        .light-theme .calculator-header {
            background: rgba(255, 255, 255, 0.5);
            color: #333;
        }
        
        .light-theme .display {
            background: rgba(255, 255, 255, 0.7);
            color: #333;
            border-bottom: 1px solid rgba(0, 0, 0, 0.1);
        }
        
        .light-theme .calculation-display {
            color: rgba(0, 0, 0, 0.7);
        }
        
        .light-theme button {
            background: rgba(255, 255, 255, 0.6);
            color: #333;
        }
        
        .light-theme button:hover {
            background: rgba(255, 255, 255, 0.9);
        }
        
        .light-theme .operator {
            background: rgba(255, 149, 0, 0.2);
            color: #ff9500;
        }
        
        .light-theme .clear, .light-theme .backspace {
            background: rgba(255, 87, 87, 0.2);
            color: #ff5757;
        }
        
        .light-theme .memory-indicator {
            background: rgba(0, 0, 0, 0.1);
            color: #333;
        }
        
        .light-theme .theme-toggle {
            background: rgba(0, 0, 0, 0.1);
            color: #333;
        }
    </style>
</head>
<body>
    <button class="theme-toggle" id="themeToggle">
        <i class="fas fa-moon"></i>
    </button>
    
    <div class="calculator-container">
        <div class="calculator-header">
            <h1>Красивый калькулятор</h1>
            <p>С современным дизайном и функциями</p>
        </div>
        
        <div class="display">
            <div class="calculation-display" id="calculation"></div>
            <div class="result-display" id="display">0</div>
        </div>
        
        <div class="memory-indicator" id="memoryIndicator">M</div>
        
        <div class="buttons">
            <button class="memory-btn" id="mc">MC</button>
            <button class="memory-btn" id="mr">MR</button>
            <button class="memory-btn" id="m-plus">M+</button>
            <button class="memory-btn" id="m-minus">M-</button>
            
            <button class="clear" id="clear">C</button>
            <button class="backspace" id="backspace"><i class="fas fa-backspace"></i></button>
            <button class="operator" data-operation="%">%</button>
            <button class="operator" data-operation="/">÷</button>
            
            <button class="number" data-number="7">7</button>
            <button class="number" data-number="8">8</button>
            <button class="number" data-number="9">9</button>
            <button class="operator" data-operation="*">×</button>
            
            <button class="number" data-number="4">4</button>
            <button class="number" data-number="5">5</button>
            <button class="number" data-number="6">6</button>
            <button class="operator" data-operation="-">-</button>
            
            <button class="number" data-number="1">1</button>
            <button class="number" data-number="2">2</button>
            <button class="number" data-number="3">3</button>
            <button class="operator" data-operation="+">+</button>
            
            <button class="number zero" data-number="0">0</button>
            <button class="number" data-number=".">.</button>
            <button class="equals" id="equals">=</button>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const display = document.getElementById('display');
            const calculationDisplay = document.getElementById('calculation');
            const buttons = document.querySelectorAll('button');
            const themeToggle = document.getElementById('themeToggle');
            const memoryIndicator = document.getElementById('memoryIndicator');
            
            let currentInput = '0';
            let previousInput = '';
            let operation = null;
            let resetScreen = false;
            let memory = 0;
            let calculationHistory = '';
            
            // Обновляем отображение
            function updateDisplay() {
                display.textContent = currentInput;
                calculationDisplay.textContent = calculationHistory;
            }
            
            // Добавляем цифру
            function appendNumber(number) {
                if (currentInput === '0' || resetScreen) {
                    currentInput = number;
                    resetScreen = false;
                } else {
                    // Проверка на максимальную длину
                    if (currentInput.length < 12) {
                        currentInput += number;
                    }
                }
            }
            
            // Добавляем десятичную точку
            function addDecimal() {
                if (resetScreen) {
                    currentInput = '0.';
                    resetScreen = false;
                    return;
                }
                
                if (!currentInput.includes('.')) {
                    currentInput += '.';
                }
            }
            
            // Обрабатываем операторы
            function handleOperator(op) {
                const inputValue = currentInput;
                
                if (operation !== null) calculate();
                
                previousInput = currentInput;
                operation = op;
                calculationHistory = `${previousInput} ${getOperatorSymbol(op)} `;
                resetScreen = true;
                
                updateDisplay();
            }
            
            // Получаем символ оператора для отображения
            function getOperatorSymbol(op) {
                switch (op) {
                    case '+': return '+';
                    case '-': return '-';
                    case '*': return '×';
                    case '/': return '÷';
                    case '%': return '%';
                    default: return op;
                }
            }
            
            // Выполняем вычисления
            function calculate() {
                let computation;
                const prev = parseFloat(previousInput);
                const current = parseFloat(currentInput);
                
                if (isNaN(prev) || isNaN(current)) return;
                
                switch (operation) {
                    case '+':
                        computation = prev + current;
                        break;
                    case '-':
                        computation = prev - current;
                        break;
                    case '*':
                        computation = prev * current;
                        break;
                    case '/':
                        if (current === 0) {
                            computation = 'Ошибка';
                        } else {
                            computation = prev / current;
                        }
                        break;
                    case '%':
                        computation = prev % current;
                        break;
                    default:
                        return;
                }
                
                // Округляем результат, если он слишком длинный
                if (computation !== 'Ошибка') {
                    computation = Math.round(computation * 100000000) / 100000000;
                    computation = computation.toString();
                    
                    // Обрезаем слишком длинные числа
                    if (computation.length > 12) {
                        computation = parseFloat(computation).toExponential(5);
                    }
                }
                
                currentInput = computation;
                calculationHistory += ` ${currentInput}`;
                operation = null;
            }
            
            // Очищаем калькулятор
            function clearCalculator() {
                currentInput = '0';
                previousInput = '';
                operation = null;
                calculationHistory = '';
            }
            
            // Удаляем последний символ
            function backspace() {
                if (currentInput.length === 1 || (currentInput.length === 2 && currentInput.startsWith('-'))) {
                    currentInput = '0';
                } else {
                    currentInput = currentInput.slice(0, -1);
                }
            }
            
            // Функции памяти
            function memoryClear() {
                memory = 0;
                memoryIndicator.style.display = 'none';
            }
            
            function memoryRecall() {
                currentInput = memory.toString();
                resetScreen = false;
            }
            
            function memoryAdd() {
                memory += parseFloat(currentInput) || 0;
                memoryIndicator.style.display = 'block';
            }
            
            function memorySubtract() {
                memory -= parseFloat(currentInput) || 0;
                memoryIndicator.style.display = 'block';
            }
            
            // Переключение темы
            themeToggle.addEventListener('click', () => {
                document.body.classList.toggle('light-theme');
                
                if (document.body.classList.contains('light-theme')) {
                    themeToggle.innerHTML = '<i class="fas fa-sun"></i>';
                } else {
                    themeToggle.innerHTML = '<i class="fas fa-moon"></i>';
                }
            });
            
            // Обработка нажатий кнопок
            buttons.forEach(button => {
                button.addEventListener('click', () => {
                    if (button.classList.contains('number')) {
                        if (button.dataset.number === '.') {
                            addDecimal();
                        } else {
                            appendNumber(button.dataset.number);
                        }
                        updateDisplay();
                    } else if (button.classList.contains('operator')) {
                        handleOperator(button.dataset.operation);
                    } else if (button.id === 'equals') {
                        if (operation) {
                            calculate();
                            updateDisplay();
                        }
                    } else if (button.id === 'clear') {
                        clearCalculator();
                        updateDisplay();
                    } else if (button.id === 'backspace') {
                        backspace();
                        updateDisplay();
                    } else if (button.id === 'mc') {
                        memoryClear();
                    } else if (button.id === 'mr') {
                        memoryRecall();
                        updateDisplay();
                    } else if (button.id === 'm-plus') {
                        memoryAdd();
                    } else if (button.id === 'm-minus') {
                        memorySubtract();
                    }
                });
            });
            
            // Обработка клавиатуры
            document.addEventListener('keydown', (event) => {
                if (/[0-9]/.test(event.key)) {
                    appendNumber(event.key);
                    updateDisplay();
                } else if (event.key === '.') {
                    addDecimal();
                    updateDisplay();
                } else if (event.key === '+' || event.key === '-' || event.key === '*' || event.key === '/') {
                    handleOperator(event.key);
                } else if (event.key === 'Enter' || event.key === '=') {
                    if (operation) {
                        calculate();
                        updateDisplay();
                    }
                } else if (event.key === 'Escape') {
                    clearCalculator();
                    updateDisplay();
                } else if (event.key === 'Backspace') {
                    backspace();
                    updateDisplay();
                } else if (event.key === '%') {
                    handleOperator('%');
                }
            });
            
            // Инициализация
            updateDisplay();
        });
    </script>
</body>
</html>
