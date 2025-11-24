# EXP 3 : IIR-CHEBYSHEV-FITER-DESIGN
## NAME   : NANCY CAROLEINE P R
## REG NO : 212223060181
## AIM: 
To design an IIR Chebyshev filter  using SCILAB. 

## APPARATUS REQUIRED: 
PC installed with SCILAB. 

## PROGRAM (LPF):
```
// === Clear Workspace ===
clc;
clear;
close();

// === User Inputs ===
fc = 1000;       // Cut-off frequency (Hz)
fs = 8000;       // Sampling frequency (Hz)
N  = 5;          // Filter order
rp = 0.5;        // Pass-band ripple (delta) for Chebyshev-I, 0 < rp < 1

// === Normalize Cutoff Frequency ===
// For Scilab’s iir, frq must lie in (0, 0.5) according to documentation :contentReference[oaicite:0]{index=0}  
f_norm = fc / fs;
if f_norm <= 0 | f_norm >= 0.5 then
    error("Normalized cutoff frequency must lie in (0, 0.5)");
end

// === Design Chebyshev Type I Low-Pass Filter ===
// iir(n, ftype, fdesign, frq, delta) :contentReference[oaicite:1]{index=1}  
hz = iir(N, "lp", "cheb1", [f_norm, 0], [rp, rp]);

// === Frequency Response ===
nPoints = 512;
[Hw, w] = frmag(hz, nPoints);
phase = atan(imag(Hw), real(Hw));

// === Plot Magnitude & Phase ===
clf();
subplot(2,1,1);
plot(w, 20 * log10(abs(Hw)), 'b');
xlabel("Normalized Frequency (× fₛ)");
ylabel("Magnitude (dB)");
title("Chebyshev Type I LPF – Magnitude Response");

// === Extract Filter Coefficients ===
// Convert transfer function to polynomials in delay operator q = z⁻¹
q = poly(0, "q");
hzd = horner(hz, 1 / q);
b = coeff(hzd.num);
a = coeff(hzd.den);

disp("Numerator coefficients b = ");
disp(b);
disp("Denominator coefficients a = ");
disp(a);
```

## PROGRAM (HPF): 
```

// === Clear Workspace ===
clc;
clear;
close();

// === User Inputs ===
fc = 1000;       // Cut-off frequency (Hz)
fs = 8000;       // Sampling frequency (Hz)
N  = 5;          // Filter order
rp = 0.5;        // Pass-band ripple (delta) for Chebyshev-I, 0 < rp < 1

// === Normalize Cutoff Frequency ===
// For Scilab’s iir, frq must lie in (0, 0.5) according to documentation
f_norm = fc / fs;
if f_norm <= 0 | f_norm >= 0.5 then
    error("Normalized cutoff frequency must lie in (0, 0.5)");
end

// === Design Chebyshev Type I High-Pass Filter ===
// iir(n, ftype, fdesign, frq, delta)
// ftype: "hp" for high-pass
hz = iir(N, "hp", "cheb1", [f_norm, 0], [rp, rp]);

// === Frequency Response ===
nPoints = 512;
[Hw, w] = frmag(hz, nPoints);
phase = atan(imag(Hw), real(Hw));

// === Plot Magnitude & Phase ===
clf();
subplot(2,1,1);
plot(w, 20 * log10(abs(Hw)), 'b');
xlabel("Normalized Frequency (× fₛ)");
ylabel("Magnitude (dB)");
title("Chebyshev Type I HPF – Magnitude Response");

// === Extract Filter Coefficients ===
// Convert transfer function to polynomials in delay operator q = z⁻¹
q = poly(0, "q");
hzd = horner(hz, 1 / q);
b = coeff(hzd.num);
a = coeff(hzd.den);

disp("Numerator coefficients b = ");
disp(b);
disp("Denominator coefficients a = ");
disp(a);
```

## OUTPUT (LPF) : 

<img width="1920" height="1080" alt="Screenshot (386)" src="https://github.com/user-attachments/assets/9f61c3fe-f352-491a-b88e-d160bcb0322a" />

## OUTPUT (HPF) : 
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/52841695-7347-4451-b73b-a931047b47fa" />

# RESULT: 
Thus Low pass filter and High pass filter were designed using Chebysev filter design
