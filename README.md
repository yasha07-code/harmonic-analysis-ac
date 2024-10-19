# harmonic-analysis-ac
import numpy as np
import matplotlib.pyplot as plt

# Sample AC signal: combination of 50 Hz (fundamental) and 150 Hz (third harmonic)
def generate_signal(t):
    return np.sin(2 * np.pi * 50 * t) + 0.3 * np.sin(2 * np.pi * 150 * t)

# Fourier Transform function
def fourier_analysis(signal, sample_rate):
    n = len(signal)
    freqs = np.fft.fftfreq(n, d=1/sample_rate)
    fft_vals = np.fft.fft(signal)
    
    # Only positive frequencies
    idx = np.where(freqs > 0)
    freqs = freqs[idx]
    fft_vals = np.abs(fft_vals[idx])
    
    return freqs, fft_vals

# Generate time vector and signal
t = np.linspace(0, 1, 1000, endpoint=False)
signal = generate_signal(t)

# Perform Fourier analysis
freqs, fft_vals = fourier_analysis(signal, 1000)

# Plotting the harmonics
plt.plot(freqs, fft_vals)
plt.title('Harmonic Components')
plt.xlabel('Frequency (Hz)')
plt.ylabel('Amplitude')
plt.grid(True)
plt.show()
