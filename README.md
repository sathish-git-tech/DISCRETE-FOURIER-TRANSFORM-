## EXP 1 A : COMPUTATION OF DFT USING DIRECT AND FFT

## AIM: 
To Obtain DFT and FFT of a given sequence in SCILAB. 

## APPARATUS REQUIRED: 
PC installed with SCILAB. 

## PROGRAM: 
// DISCRETE FOURIER TRANSFORM 
```
clc;
clear;

// Use a test signal if input is causing issues
N = 8;
x = [1, 1, 1, 1, 1, 1, 1, 1];  // Rectangular pulse

disp("Using test signal: x = " + string(x));

// Compute DFT
X = zeros(1, N);
for k = 0:N-1
    sum_val = 0;
    for n = 0:N-1
        sum_val = sum_val + x(n+1) * exp(-%i * 2 * %pi * k * n / N);
    end
    X(k+1) = sum_val;
end

// Display results
disp("DFT Results:");
for k = 0:N-1
    printf("X(%d) = %.3f + j%.3f\n", k, real(X(k+1)), imag(X(k+1)));
end

// Create a new figure window
f = scf(0);
f.figure_name = "DFT Analysis";
clf(0);

// Plot input signal
subplot(3,1,1);
plot2d3(0:N-1, x, style=2);  // Blue stems
xlabel("Time index (n)");
ylabel("Amplitude");
title("Input Signal x[n]");

// Plot magnitude spectrum
subplot(3,1,2);
plot2d3(0:N-1, abs(X), style=5);  // Red stems
xlabel("Frequency index (k)");
ylabel("|X(k)|");
title("Magnitude Spectrum");

// Plot phase spectrum
subplot(3,1,3);
plot2d3(0:N-1, atan(imag(X), real(X)), style=3);  // Green stems
xlabel("Frequency index (k)");
ylabel("Phase (radians)");
title("Phase Spectrum");

// Ensure window is visible
show_window(0);
```
//FFT
```
clc;
clear;

// Step 1: Take N and x(n) as input
N = input("Enter the length of the signal N (power of 2): ");
x = zeros(1, N);

disp("Enter the signal values:");
for i = 1:N
    x(i) = input("x(" + string(i-1) + ") = ");
end

// Step 2: Bit-reversal reordering
function rev = bit_reverse_index(idx, logN)
    bin_str = dec2bin(idx, logN); // binary string of length logN
    rev_str = strrev(bin_str);    // reverse it
    rev = bin2dec(rev_str);       // back to decimal
endfunction

logN = log2(N);
X = zeros(1, N);

for i = 0:N-1
    rev_idx = bit_reverse_index(i, logN);
    X(rev_idx+1) = x(i+1);
end

// Step 3: FFT using DIT butterfly
m = 1;
for s = 1:logN
    m = 2^s;
    wm = exp(-%i*2*%pi/m);
    for k = 0:(N/m - 1)
        for j = 0:(m/2 - 1)
            t = wm^j * X(k*m + j + m/2 + 1);
            u = X(k*m + j + 1);
            X(k*m + j + 1)       = u + t;
            X(k*m + j + m/2 + 1) = u - t;
        end
    end
end

// Step 4: Display in desired { a ± jb } format
str_out = "{";
for k = 1:N
    real_part = round(real(X(k))*1000)/1000; // rounding to 3 decimals
    imag_part = round(imag(X(k))*1000)/1000;
    
    if imag_part >= 0 then
        str_out = str_out + string(real_part) + " + j" + string(imag_part);
    else
        str_out = str_out + string(real_part) + " - j" + string(abs(imag_part));
    end
    
    if k < N then
        str_out = str_out + ", ";
    else
        str_out = str_out + "}";
    end
end

disp("X(k) = " + str_out);

// Step 5: Plot magnitude and phase (DISCRETE TIME)
freq_index = 0:N-1;

subplot(2,1,1);
plot2d3(freq_index, abs(X));  // discrete stem-like plot
xlabel("Frequency index (k)");
ylabel("|X(k)|");
title("Magnitude Spectrum using DIT-FFT");

subplot(2,1,2);
plot2d3(freq_index, atan(imag(X), real(X))); // atan2(imag, real)
xlabel("Frequency index (k)");
ylabel("Phase (radians)");
title("Phase Spectrum using DIT-FFT");

```

## OUTPUT: 
<img width="765" height="725" alt="Screenshot 2025-08-28 141302" src="https://github.com/user-attachments/assets/96291705-ca80-4598-a71c-0cbe450fee34" />
<img width="765" height="725" alt="Screenshot 2025-08-28 141041" src="https://github.com/user-attachments/assets/442fd71c-8caf-4364-a697-99eb5220094d" />

## RESULT: 
The DFT of the given sequence was successfully computed using both direct computation method and FFT algorithm in SCILAB.

