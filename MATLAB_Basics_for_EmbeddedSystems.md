# MATLAB Basics for Embedded Systems & IoT Engineering

## Overview
This guide covers essential MATLAB concepts for mechanical engineers transitioning to embedded systems and IoT. You'll learn how MATLAB can prototype, simulate, and control embedded applications.

---

## Table of Contents
1. [Introduction & Why MATLAB for Embedded Systems](#introduction)
2. [Basic Concepts](#basic-concepts)
3. [Variables and Data Types](#variables-and-data-types)
4. [Arrays and Matrices](#arrays-and-matrices)
5. [Operators and Operations](#operators-and-operations)
6. [Control Flow](#control-flow)
7. [Functions](#functions)
8. [Data Visualization](#data-visualization)
9. [File I/O and Data Handling](#file-io)
10. [Practical Examples for IoT](#practical-examples)

---

## Introduction & Why MATLAB for Embedded Systems

MATLAB is widely used in embedded systems development for:
- **Prototyping algorithms** before deploying on microcontrollers
- **Simulation and modeling** of sensors and actuators
- **Real-time processing** of sensor data
- **Control systems design** (crucial for robotics, motor control, etc.)
- **Hardware integration** via Arduino, Raspberry Pi, and other platforms

### Your Journey: Mechanical → Embedded Systems
- **Mechanical Design**: You understand physical systems, mechanics, dynamics
- **Embedded Systems**: You'll now control these systems programmatically
- **MATLAB's Role**: Bridge between theoretical understanding and real hardware

---

## Basic Concepts

### What is MATLAB?
MATLAB = **MAT**rix **LAB**oratory. It's a numerical computing environment designed for matrix operations, but now it's a complete ecosystem for algorithm development, simulation, and hardware integration.

### The MATLAB Environment
- **Command Window**: Type commands directly (like a calculator)
- **Editor**: Write scripts and functions
- **Workspace**: View all your variables
- **Command History**: See previous commands

### Your First Command
```matlab
% This is a comment
disp('Hello, Embedded Systems World!')  % Display text
```

---

## Variables and Data Types

### Creating Variables
Variables store data. MATLAB is dynamically typed (you don't need to declare type beforehand).

```matlab
% Numbers
temperature = 25.5;        % Float
sensor_count = 5;          % Integer
pi_value = pi;             % Built-in constant

% Strings
device_name = "Arduino";
message = 'IoT Sensor';

% Logical (Boolean)
is_active = true;
sensor_ready = false;

% Display variables
disp(temperature)
disp(device_name)
```

### Understanding Basic Data Types

| Type | Example | Use Case |
|------|---------|----------|
| **Double** | `3.14`, `temperature` | Floating-point calculations (sensor readings) |
| **Int** | `5`, `counter` | Integer counting (loop counters) |
| **String** | `"sensor_01"` | Device names, labels |
| **Logical** | `true`, `false` | Boolean flags, conditions |

---

## Arrays and Matrices

Since MATLAB is a matrix lab, arrays are fundamental. As an embedded engineer, you'll use arrays for:
- Storing sensor readings over time
- Processing multiple sensor values
- Image/signal processing data

### Creating Arrays

```matlab
% Row vector (1D array - horizontal)
sensor_data = [23.5, 24.1, 23.8, 24.3, 25.0];

% Column vector (1D array - vertical)
voltage = [5.0; 4.9; 5.1; 4.8]';

% Or using semicolon
voltage = [5.0; 4.9; 5.1; 4.8];

% Matrix (2D array)
sensor_matrix = [1, 2, 3; 
                 4, 5, 6; 
                 7, 8, 9];

% Generate arrays efficiently
time = 0:0.1:1.0;              % Start:Step:End → [0, 0.1, 0.2, ..., 1.0]
ones_array = ones(1, 5);       % Row of 5 ones
zeros_array = zeros(3, 3);     % 3×3 matrix of zeros
random_data = rand(1, 100);    % 100 random values (0-1)
```

### Accessing Array Elements

```matlab
sensor_data = [23.5, 24.1, 23.8, 24.3, 25.0];

first_reading = sensor_data(1);        % First element
last_reading = sensor_data(end);       % Last element
middle_readings = sensor_data(2:4);    % Elements 2 to 4
every_other = sensor_data(1:2:end);    % Every other element

% Matrix indexing
matrix = [1, 2, 3; 4, 5, 6; 7, 8, 9];
element = matrix(2, 3);                % Row 2, Column 3 → 6
row_2 = matrix(2, :);                  % All of row 2
column_1 = matrix(:, 1);               % All of column 1
```

### Array Operations

```matlab
a = [1, 2, 3];
b = [4, 5, 6];

% Element-wise operations (use . before operator)
sum_elements = a + b;          % [5, 7, 9]
product_elements = a .* b;     % [4, 10, 18]
division = a ./ b;            % [0.25, 0.4, 0.5]
power = a .^ 2;               % [1, 4, 9]

% Statistical functions
mean_value = mean(a);          % Average
max_value = max(a);            % Maximum
min_value = min(a);            % Minimum
sum_total = sum(a);            % Sum of all elements
std_dev = std(a);              % Standard deviation
```

---

## Operators and Operations

### Arithmetic Operators

```matlab
a = 10;
b = 3;

addition = a + b;              % 13
subtraction = a - b;           % 7
multiplication = a * b;        % 30
division = a / b;              % 3.3333
power = a ^ b;                 % 1000 (10 to the power 3)
modulo = mod(a, b);            % 1 (remainder)
```

### Comparison Operators
These return true (1) or false (0).

```matlab
a = 5;
b = 3;

a > b;                         % true (1)
a < b;                         % false (0)
a == b;                        % false (0)
a ~= b;                        % true (1) - not equal
a >= b;                        % true (1)
a <= b;                        % false (0)
```

### Logical Operators
Combine multiple conditions.

```matlab
temp = 25;
humidity = 60;

% AND operator
condition1 = (temp > 20) && (temp < 30);      % true
condition2 = (temp > 30) && (humidity < 70);  % false

% OR operator
condition3 = (temp > 30) || (humidity > 50);  % true

% NOT operator
condition4 = ~(temp < 0);                     % true
```

---

## Control Flow

### If-Else Statements
Execute code conditionally - essential for sensor decision-making.

```matlab
% Simple if
temperature = 28;

if temperature > 30
    disp('Temperature is high - activate cooling');
end

% If-Else
if temperature > 30
    disp('Hot - turn on cooler');
elseif temperature < 20
    disp('Cold - turn on heater');
else
    disp('Temperature is comfortable');
end

% Nested if (multiple conditions)
sensor_value = 150;
if sensor_value > 100
    if sensor_value > 200
        disp('Critical level');
    else
        disp('Warning level');
    end
else
    disp('Normal level');
end
```

### For Loops
Repeat code a specific number of times - perfect for processing multiple sensor readings.

```matlab
% Basic for loop
for i = 1:5
    disp(i);  % Print 1, 2, 3, 4, 5
end

% Loop through array
sensor_data = [23.5, 24.1, 23.8, 24.3, 25.0];
for idx = 1:length(sensor_data)
    disp(sensor_data(idx));
end

% Loop through array directly (more elegant)
for reading in sensor_data
    disp(reading);
end

% Nested loops (processing 2D data like sensor arrays)
matrix = [1, 2, 3; 4, 5, 6; 7, 8, 9];
for row = 1:3
    for col = 1:3
        element = matrix(row, col);
        disp(['Element at (' num2str(row) ',' num2str(col) ') = ' num2str(element)]);
    end
end
```

### While Loops
Repeat code while a condition is true - useful for sensor polling or waiting for events.

```matlab
% Simple while loop
count = 0;
while count < 5
    disp(['Count: ' num2str(count)]);
    count = count + 1;  % Must increment to avoid infinite loop
end

% Real-world example: Wait for sensor reading
sensor_value = 0;
timeout = 100;  % Maximum iterations
while sensor_value < 500 && timeout > 0
    sensor_value = sensor_value + 50;  % Simulate sensor reading
    timeout = timeout - 1;
    disp(['Sensor value: ' num2str(sensor_value)]);
end
```

### Break and Continue

```matlab
% Break: Exit loop early
for i = 1:10
    if i == 5
        break;  % Exit when i equals 5
    end
    disp(i);  % Prints 1, 2, 3, 4
end

% Continue: Skip to next iteration
for i = 1:5
    if i == 3
        continue;  % Skip i = 3
    end
    disp(i);  % Prints 1, 2, 4, 5
end
```

---

## Functions

Functions are reusable blocks of code - essential for embedded systems where you have repeated tasks.

### Basic Function Structure

```matlab
function [output1, output2] = function_name(input1, input2)
    % Function documentation
    % This function does something
    
    % Function body
    output1 = input1 + input2;
    output2 = input1 * input2;
end
```

### Simple Examples

```matlab
% Function to convert Celsius to Fahrenheit
function fahrenheit = celsiusToFahrenheit(celsius)
    fahrenheit = (celsius * 9/5) + 32;
end

% Usage
temp_c = 25;
temp_f = celsiusToFahrenheit(temp_c);
disp(['25°C = ' num2str(temp_f) '°F']);  % Output: 25°C = 77°F

% Function with multiple outputs
function [mean_val, std_val] = analyzeData(data)
    mean_val = mean(data);
    std_val = std(data);
end

% Usage
sensor_readings = [20.1, 20.5, 20.3, 20.7, 20.4];
[avg, std_dev] = analyzeData(sensor_readings);
disp(['Average: ' num2str(avg) ', Std Dev: ' num2str(std_dev)]);

% Function with optional parameters (variable arguments)
function displayStatus(device_name, varargin)
    disp(['Device: ' device_name]);
    
    if nargin > 1
        status = varargin{1};
        disp(['Status: ' status]);
    end
end

% Usage
displayStatus('Sensor_01');
displayStatus('Sensor_01', 'Active');
```

### Real-World IoT Example

```matlab
function alert_status = checkSensorThreshold(sensor_value, min_threshold, max_threshold)
    % Check if sensor reading is within acceptable range
    % Inputs: sensor_value, min_threshold, max_threshold
    % Output: alert_status ('OK', 'LOW', or 'HIGH')
    
    if sensor_value < min_threshold
        alert_status = 'LOW';
    elseif sensor_value > max_threshold
        alert_status = 'HIGH';
    else
        alert_status = 'OK';
    end
end

% Usage
temp = 32;
status = checkSensorThreshold(temp, 18, 28);
disp(status);  % Output: HIGH
```

---

## Data Visualization

Visualizing data is crucial for understanding sensor behavior and debugging embedded systems.

### Basic Plotting

```matlab
% Time series data (simulate 10 seconds of temperature readings)
time = 0:0.1:10;
temperature = 20 + 5*sin(time) + randn(size(time))*0.5;  % Simulated data

% Plot
plot(time, temperature, 'b-', 'LineWidth', 2);  % Blue solid line
xlabel('Time (seconds)');
ylabel('Temperature (°C)');
title('Temperature Over Time');
grid on;  % Add gridlines
```

### Multiple Plots

```matlab
time = 0:0.1:10;
temp = 20 + 5*sin(time);
humidity = 50 + 10*cos(time);

% Subplots
subplot(2, 1, 1);  % 2 rows, 1 column, plot 1
plot(time, temp, 'r-');
xlabel('Time (s)');
ylabel('Temperature (°C)');
title('Temperature vs Time');
grid on;

subplot(2, 1, 2);  % 2 rows, 1 column, plot 2
plot(time, humidity, 'b-');
xlabel('Time (s)');
ylabel('Humidity (%)');
title('Humidity vs Time');
grid on;
```

### Different Plot Types

```matlab
% Bar chart (e.g., sensor readings at different locations)
sensors = {'Room1', 'Room2', 'Room3', 'Room4'};
readings = [22.5, 23.1, 21.8, 24.2];
bar(readings);
set(gca, 'xticklabel', sensors);
ylabel('Temperature (°C)');
title('Temperature in Different Rooms');

% Scatter plot (e.g., voltage vs current)
voltage = [5, 10, 15, 20, 25];
current = [0.5, 1.0, 1.5, 2.0, 2.5];
scatter(voltage, current, 'filled');
xlabel('Voltage (V)');
ylabel('Current (A)');
title('Voltage vs Current');

% Histogram (e.g., distribution of sensor readings)
sensor_data = randn(1000, 1) * 2 + 25;  % Normally distributed data
histogram(sensor_data, 20);
xlabel('Temperature (°C)');
ylabel('Frequency');
title('Distribution of Sensor Readings');
```

---

## File I/O and Data Handling

Embedded systems often need to log data or read configuration files.

### Writing Data to File

```matlab
% Create sample data
timestamp = [1, 2, 3, 4, 5]';
temperature = [20.1, 20.5, 20.3, 20.7, 20.4]';
humidity = [45, 48, 47, 49, 46]';

% Create table
data_table = table(timestamp, temperature, humidity);

% Write to CSV file
writetable(data_table, 'sensor_log.csv');

% Or write using simple fprintf
fid = fopen('sensor_log.txt', 'w');
fprintf(fid, 'Time,Temp,Humidity\n');
for i = 1:length(timestamp)
    fprintf(fid, '%d,%.1f,%d\n', timestamp(i), temperature(i), humidity(i));
end
fclose(fid);
```

### Reading Data from File

```matlab
% Read CSV file
data_table = readtable('sensor_log.csv');

% Access columns
temps = data_table.temperature;
times = data_table.timestamp;

% Read text file
fid = fopen('sensor_log.txt', 'r');
header = fgetl(fid);  % Read header
data = fscanf(fid, '%d,%f,%d\n');  % Read data
fclose(fid);
```

---

## Practical Examples for IoT

### Example 1: Temperature Monitoring System

```matlab
% Simulate an IoT temperature sensor monitoring system

function tempMonitoringDemo()
    % Parameters
    num_readings = 60;  % 60 temperature readings
    sampling_interval = 1;  % 1 second between readings
    temp_threshold_high = 28;
    temp_threshold_low = 18;
    
    % Initialize arrays
    time = (0:num_readings-1) * sampling_interval;
    % Simulate temperature with sine wave + noise
    base_temp = 23;
    temperature = base_temp + 3*sin(2*pi*time/60) + randn(1, num_readings)*0.5;
    
    % Process data
    alerts = zeros(1, num_readings);
    for i = 1:num_readings
        if temperature(i) > temp_threshold_high
            alerts(i) = 2;  % High alert
        elseif temperature(i) < temp_threshold_low
            alerts(i) = 1;  % Low alert
        else
            alerts(i) = 0;  % Normal
        end
    end
    
    % Visualization
    figure('Name', 'IoT Temperature Monitoring');
    
    % Plot temperature
    subplot(2, 1, 1);
    plot(time, temperature, 'b-', 'LineWidth', 2);
    hold on;
    yline(temp_threshold_high, 'r--', 'High Threshold');
    yline(temp_threshold_low, 'g--', 'Low Threshold');
    xlabel('Time (seconds)');
    ylabel('Temperature (°C)');
    title('Real-Time Temperature Monitoring');
    legend('Temperature', 'High Threshold', 'Low Threshold');
    grid on;
    
    % Plot alerts
    subplot(2, 1, 2);
    bar(time, alerts);
    ylabel('Alert Level');
    title('Alert Status (0=Normal, 1=Low, 2=High)');
    ylim([-0.5, 2.5]);
    grid on;
    
    % Display statistics
    disp('=== Temperature Monitoring Report ===');
    disp(['Average Temperature: ' num2str(mean(temperature), '%.2f') '°C']);
    disp(['Max Temperature: ' num2str(max(temperature), '%.2f') '°C']);
    disp(['Min Temperature: ' num2str(min(temperature), '%.2f') '°C']);
    disp(['High Alerts: ' num2str(sum(alerts == 2))]);
    disp(['Low Alerts: ' num2str(sum(alerts == 1))]);
end

% Run the demo
tempMonitoringDemo();
```

### Example 2: Sensor Data Filtering

```matlab
% Moving average filter (commonly used in embedded systems)
function filtered_data = movingAverageFilter(data, window_size)
    filtered_data = [];
    
    for i = 1:length(data) - window_size + 1
        window = data(i:i + window_size - 1);
        avg = mean(window);
        filtered_data = [filtered_data, avg];
    end
end

% Usage
raw_sensor_data = [20.1, 20.8, 20.2, 21.5, 20.9, 21.2, 20.5, 21.8, 20.7];
filtered = movingAverageFilter(raw_sensor_data, 3);

disp('Raw data: ');
disp(raw_sensor_data);
disp('Filtered data (3-point average): ');
disp(filtered);

% Plot comparison
figure;
plot(raw_sensor_data, 'ro-', 'DisplayName', 'Raw Data');
hold on;
plot([1.5:length(filtered)+0.5], filtered, 'bs-', 'DisplayName', 'Filtered Data');
xlabel('Sample Number');
ylabel('Temperature (°C)');
title('Raw vs Filtered Sensor Data');
legend;
grid on;
```

### Example 3: PWM Signal Generation (Motor Control)

```matlab
% PWM (Pulse Width Modulation) is crucial for embedded systems
function pwmSignal()
    % Parameters
    frequency = 1000;  % 1 kHz PWM frequency
    duty_cycle = 50;   % 50% duty cycle
    duration = 0.01;   % 10 milliseconds
    
    % Time array
    time = 0:1/(frequency*100):duration;
    
    % Generate PWM signal
    period = 1/frequency;
    pwm = square(2*pi*frequency*time);
    pwm = (pwm + 1) / 2;  % Convert to 0-1 range
    
    % Apply duty cycle
    pwm(pwm < duty_cycle/100) = 0;
    pwm(pwm >= duty_cycle/100) = 1;
    
    % Plot
    figure;
    plot(time*1000, pwm, 'b-', 'LineWidth', 1.5);
    xlabel('Time (ms)');
    ylabel('PWM Signal (0-1)');
    title(['PWM Signal: ' num2str(frequency) ' Hz, ' num2str(duty_cycle) '% Duty Cycle']);
    ylim([-0.2, 1.2]);
    grid on;
end

pwmSignal();
```

---

## Best Practices for Embedded Systems Development

1. **Keep Functions Modular**: Each function should do one thing well
2. **Use Meaningful Variable Names**: `motor_speed` is better than `ms`
3. **Comment Your Code**: Especially complex logic
4. **Validate Inputs**: Check for realistic sensor ranges
5. **Use Arrays for Efficiency**: Avoid loops when vectorized operations exist
6. **Log Data**: Always maintain sensor logs for debugging
7. **Test Edge Cases**: What if a sensor fails or returns 0?

---

## Common MATLAB Shortcuts

```matlab
% Helpful keyboard shortcuts
Ctrl+C          % Stop running program
Ctrl+S          % Save file
F5              % Run script
clc             % Clear command window
clear all       % Clear all variables
close all       % Close all figures

% Useful commands
help(function_name)     % Get help on function
doc(function_name)      % Open documentation
whos                    % Show all variables with info
```

---

## Next Steps

1. **Start Simple**: Modify the examples above
2. **Hardware Integration**: Learn to connect MATLAB with Arduino or Raspberry Pi
3. **Real-Time Processing**: Explore Simulink for real-time simulation
4. **Advanced Topics**: Signal processing, control systems design, machine learning
5. **GitHub**: Commit your practice code and build your portfolio

---

## Resources for Further Learning

- **MATLAB Official Documentation**: https://www.mathworks.com/help/
- **Arduino + MATLAB**: IoT and embedded systems integration
- **Simulink**: Model-based design for embedded systems
- **MATLAB Cody**: Coding challenges to improve skills
- **GitHub Projects**: Learn from other embedded systems projects

---

## License and Notes

This guide is designed for self-learning and educational purposes. As you progress to embedded systems and IoT, you'll apply these fundamentals in real hardware projects.

Good luck on your journey from mechanical design to embedded systems engineering! 🚀
