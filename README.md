# Linear-Block-Code
# Aim
Write a simple python program to Generate Matrix, Codeword, Hamming weight, Syndrome matrix and find the error on received codeword using Linear block code. 
# Tools required
# Program
```python
import numpy as np

pb = []
col = int(input("Enter the Parity bits : "))      # n-k
row = int(input("Enter the Message bits : "))     # k
for i in range(row):
    p = list(map(int, input(f"Enter row {i+1} (space separated) : ").split()))
    pb.append(p)

P = np.array(pb, dtype=int)
I_k = np.eye(row, dtype=int)
G = np.hstack((P, I_k))

print("\nGenerator Matrix (G):")
for r in G:
    print(" ".join(map(str, r)))
k = row
n = G.shape[1]
messages = np.array([[int(x) for x in format(i, f'0{k}b')] for i in range(2**k)])
codewords = np.mod(np.dot(messages, G), 2)

print("\nMessage   Codeword   Weight")
weights = []

for i in range(len(messages)):
    wt = np.sum(codewords[i])
    weights.append(wt)
    print(" ".join(map(str, messages[i])), "   ",
          " ".join(map(str, codewords[i])), "   ", wt)
d_min = np.min([w for w in weights if w != 0])
print("\nMinimum Hamming Distance:", d_min)

I_r = np.eye(col, dtype=int)
H = np.hstack((I_r, P.T))

print("\nParity Check Matrix (H):")
for r in H:
    print(" ".join(map(str, r)))

H_T = H.T
rc = list(map(int, input("\nEnter the received codeword : ").split()))
r = np.array(rc)
S = np.mod(np.dot(r, H_T), 2)

print("Syndrome :", " ".join(map(str, S)))
error = np.zeros(n, dtype=int)

for i in range(n):
    if np.array_equal(H_T[i], S):
        error[i] = 1
        break

print("Error Vector :", " ".join(map(str, error)))

corrected = np.mod(r + error, 2)
print("Corrected Codeword :", " ".join(map(str, corrected)))
```
# Output 

<img width="607" height="721" alt="image" src="https://github.com/user-attachments/assets/acfd14f8-5991-406d-a7f4-eb73b29212b5" />

# Results
Thus linear block code operation for the given input is successfully verified.
