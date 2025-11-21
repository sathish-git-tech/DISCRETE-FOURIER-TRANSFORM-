# EXP 1 A :COMPUTATION OF DFT USING DIRECT AND FFT

# AIM: 

To Obtain DFT and FFT of a given sequence in SCILAB. 

# APPARATUS REQUIRED: 
PC installed with SCILAB. 

# PROGRAM: 
``` 
// DISCRETE FOURIER TRANSFORM

clc;
clear;
x = [1 2 3 4];
N = length(x);
n = 0:N-1;
X = zeros(1,N);

for k = 0:N-1
    for m = 0:N-1
        X(k+1) = X(k+1) + x(m+1)exp(-%i*2%pi*k*m/N);
    end
end

Y = fft(x,-1);

figure;
subplot(3,1,1);
plot2d3(n,x);
xlabel("n"); ylabel("x[n]");
title("Input Sequence");

subplot(3,1,2);
plot2d3(n,abs(X));
xlabel("k"); ylabel("|X(k)|");
title("DFT Magnitude Spectrum (Direct)");

subplot(3,1,3);
plot2d3(n,abs(Y));
xlabel("k"); ylabel("|Y(k)|");
title("FFT Magnitude Spectrum (Built-in)");
```

# OUTPUT: 

<img width="447" height="426" alt="image" src="https://github.com/user-attachments/assets/3f52fc59-3293-4589-bd00-62f6b82e08bc" />

# RESULT: 
DFT and FFT of a given sequence in SCILAB
