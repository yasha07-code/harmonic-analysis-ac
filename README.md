def calculate_thd(fft_vals, fundamental_idx):
    fundamental = fft_vals[fundamental_idx]
    harmonics = np.sum(fft_vals[fundamental_idx + 1:] ** 2)
    thd = np.sqrt(harmonics) / fundamental
    return thd

# Assuming 50 Hz is the fundamental frequency (index 50 for a 1000 Hz sample rate)
fundamental_idx = np.argmax(freqs >= 50)
thd = calculate_thd(fft_vals, fundamental_idx)

print(f"Total Harmonic Distortion (THD): {thd * 100:.2f}%")

# Plot the result (add this to Fourier analysis plot)
plt.plot(freqs, fft_vals)
plt.title(f'Harmonic Components and THD: {thd * 100:.2f}%')
plt.xlabel('Frequency (Hz)')
plt.ylabel('Amplitude')
plt.grid(True)
plt.show()
