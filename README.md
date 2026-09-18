# Pemograman_Chusnu-Izza-Eziza-Faricha_Bismuth_TLS26
Tugas Pemrograman Dasar - Luminous Quest TLS 2026. Berisi implementasi C++ untuk dua problem: simulasi eliminasi melingkar dengan nilai K dinamis (The Last Astronaut) dan enkripsi pesan dengan sistem pergeseran huruf berbasis alfabet (Alien-In-The-Middle)

Problem 1

#include <iostream>

int getLength(const char str[]) {
    int len = 0;
    while (str[len] != '\0') {
        len++;
    }
    return len;}

int main() {
    int n, k;
    std::cout << "Masukkan jumlah astronot: ";
    std::cin >> n;
    std::cout << "Masukkan nilai awal: ";
    std::cin >> k;

    if (n <= 0) {
        std::cout << "Jumlah astronot harus lebih dari 0." << std::endl;
        return 0;
    }

    int astronauts[1000];
    for (int i = 0; i < n; i++) {
        astronauts[i] = i + 1;
    }

    int current_size = n;
    int current_idx = 0;

    std::cout << "\nUrutan eliminasi:" << std::endl;

    while (current_size > 1) {
        
        current_idx = (current_idx + k - 1) % current_size;
        int eliminated = astronauts[current_idx];

        std::cout << "Astronot nomor " << eliminated << " dieliminasi." << std::endl;

        
        for (int i = current_idx; i < current_size - 1; i++) {
            astronauts[i] = astronauts[i + 1];
        }
        current_size--;

        
        if (eliminated % 2 == 0) {
            k += 2;
        } else {
            k -= 1;
        }

        if (k < 2) {
            k = 2;
        }
    }

    std::cout << "\nAstronot terakhir yang bertahan: " << astronauts[0] << std::endl;

    return 0;
}


Problem 2

#include <iostream>

char toUpper(char c) {
    if (c >= 'a' && c <= 'z') {
        return c - ('a' - 'A');
    }
    return c;
}

int main() {
    char input[1000];
    std::cout << "Pesan Asli: ";
    std::cin >> input;

    char result[1000];
    int i = 0;

    while (input[i] != '\0') {
        char current = toUpper(input[i]);

        if (current >= 'A' && current <= 'Z') {
            if (i == 0) {
                result[i] = current;
            } else {
                char prev = toUpper(input[i - 1]);
                int shift = prev - 'A' + 1;

                int orig_val = current - 'A';
                int new_val = (orig_val + shift) % 26;
                result[i] = (char)('A' + new_val);
            }
        } else {
            result[i] = current;
        }
        i++;
    }
    result[i] = '\0';

    std::cout << "Pesan terenkripsi: " << result << std::endl;

    return 0;
}
