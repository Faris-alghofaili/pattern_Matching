import time

def brute_force_search(text, pattern):
    n = len(text)
    m = len(pattern)
    for i in range(n - m + 1):
        j = 0
        while j < m and text[i + j] == pattern[j]:
            j += 1
        if j == m:
            return i  # Match found at index i
    return -1  # No match found

def compute_LPS_array(pattern, m, lps):
    length = 0
    lps[0] = 0
    i = 1
    while i < m:
        if pattern[i] == pattern[length]:
            length += 1
            lps[i] = length
            i += 1
        else:
            if length != 0:
                length = lps[length - 1]
            else:
                lps[i] = 0
                i += 1

def KMP_search(text, pattern):
    m = len(pattern)
    n = len(text)
    lps = [0] * m
    compute_LPS_array(pattern, m, lps)
    i = j = 0
    while i < n:
        if pattern[j] == text[i]:
            i += 1
            j += 1
        if j == m:
            return i - j  # Match found at index (i - j)
        elif i < n and pattern[j] != text[i]:
            if j != 0:
                j = lps[j - 1]
            else:
                i += 1
    return -1  # No match found

def boyer_moore_search(text, pattern):
    m = len(pattern)
    n = len(text)
    bad_char = [-1] * 256
    for i in range(m):
        bad_char[ord(pattern[i])] = i
    s = 0
    while s <= n - m:
        j = m - 1
        while j >= 0 and pattern[j] == text[s + j]:
            j -= 1
        if j < 0:
            return s  # Match found at index s
            s += (s + m < n and m - bad_char[ord(text[s + m])] or 1)
        else:
            s += max(1, j - bad_char[ord(text[s + j])])
    return -1  # No match found


with open("text.txt", "r") as file:
    text = file.read()

with open("pattern.txt", "r") as file:
    pattern = file.read()


start_time = time.time()
bf_result = brute_force_search(text, pattern)
bf_time = time.time() - start_time

start_time = time.time()
kmp_result = KMP_search(text, pattern)
kmp_time = time.time() - start_time

start_time = time.time()
bm_result = boyer_moore_search(text, pattern)
bm_time = time.time() - start_time


print("Brute Force Result:", bf_result, "Time:", bf_time)
print("KMP Result:", kmp_result, "Time:", kmp_time)
print("Boyer Moore Result:", bm_result, "Time:", bm_time)
