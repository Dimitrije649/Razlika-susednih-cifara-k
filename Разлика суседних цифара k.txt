#include <bits/stdc++.h> 

using namespace std;

int n, k;
vector<string> res; 

// Rekurzivna funkcija za generisanje brojeva
void generisi(int pozicija, int prethodna_cifra, string broj) {
    if (pozicija == n) { // Ako smo napravili broj dužine n
        res.push_back(broj); // Dodajemo ga u rezultate
        return;
    }

    // Definišemo moguće razlike u zavisnosti od k
    vector<int> deltas = (k == 0) ? vector<int>{0} : vector<int>{-k, k};

    for (int delta : deltas) {
        int nova_cifra = prethodna_cifra + delta; // Sledeća cifra na osnovu razlike
        if (nova_cifra >= 0 && nova_cifra <= 9) { // Mora biti validna cifra
            // Rekurzivno gradimo dalje broj
            generisi(pozicija + 1, nova_cifra, broj + to_string(nova_cifra));
        }
    }
}

int main() {
    cin >> n >> k; // Unos dužine broja i razlike

    // Prva cifra ne može biti 0, pa krećemo od 1 do 9
    for (int prva_cifra = 1; prva_cifra <= 9; ++prva_cifra) {
        generisi(1, prva_cifra, to_string(prva_cifra)); // Krećemo od prve cifre
    }

    // Sortiramo rezultate da bi ispis bio u rastućem redosledu
    sort(res.begin(), res.end());

    // Ispis svih validnih brojeva
    for (const string& broj : res) {
        cout << broj << '\n';
    }

    return 0;
}