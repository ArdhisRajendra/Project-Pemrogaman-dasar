# Project-Pemrogaman-dasar

#include <iostream>
#include <vector>
#include <string>
#include <algorithm>
using namespace std;

// Struktur data untuk Kereta Api
struct KeretaApi {
    string kode;
    string nama;
    string asal;
    string tujuan;
    string jadwal_keberangkatan;
    string jadwal_kedatangan;
    int jumlah_gerbong;
    vector<string> penumpang;
};

// Prosedur untuk menampilkan informasi kereta
void tampilkanInformasi(const KeretaApi& kereta) {
    cout << "\n--- Informasi Kereta ---\n";
    cout << "Kode: " << kereta.kode << endl;
    cout << "Nama: " << kereta.nama << endl;
    cout << "Asal: " << kereta.asal << endl;
    cout << "Tujuan: " << kereta.tujuan << endl;
    cout << "Jadwal: " << kereta.jadwal_keberangkatan << " - " << kereta.jadwal_kedatangan << endl;
    cout << "Jumlah Gerbong: " << kereta.jumlah_gerbong << endl;
    cout << "Jumlah Penumpang: " << kereta.penumpang.size() << endl;
}

// Prosedur untuk menambah gerbong
void tambahGerbong(KeretaApi& kereta, int jumlah) {
    kereta.jumlah_gerbong += jumlah;
    cout << "Gerbong berhasil ditambahkan. Total gerbong sekarang: " << kereta.jumlah_gerbong << endl;
}

// Prosedur untuk mengubah jadwal
void ubahJadwal(KeretaApi& kereta, const string& keberangkatan, const string& kedatangan) {
    kereta.jadwal_keberangkatan = keberangkatan;
    kereta.jadwal_kedatangan = kedatangan;
    cout << "Jadwal berhasil diubah menjadi: " << keberangkatan << " - " << kedatangan << endl;
}

// Prosedur untuk menambah penumpang
void tambahPenumpang(KeretaApi& kereta, const string& nama) {
    kereta.penumpang.push_back(nama);
    cout << "Penumpang " << nama << " berhasil ditambahkan." << endl;
}

// Prosedur untuk menghapus penumpang
void hapusPenumpang(KeretaApi& kereta, const string& nama) {
    auto it = find(kereta.penumpang.begin(), kereta.penumpang.end(), nama); // Menggunakan std::find
    if (it != kereta.penumpang.end()) {
        kereta.penumpang.erase(it);
        cout << "Penumpang " << nama << " berhasil dihapus." << endl;
    } else {
        cout << "Penumpang " << nama << " tidak ditemukan." << endl;
    }
}

// Prosedur untuk menampilkan daftar penumpang
void daftarPenumpang(const KeretaApi& kereta) {
    cout << "\n--- Daftar Penumpang ---\n";
    if (kereta.penumpang.empty()) {
        cout << "Tidak ada penumpang.\n";
    } else {
        for (const auto& nama : kereta.penumpang) {
            cout << "- " << nama << endl;
        }
    }
}

int main() {
    KeretaApi kereta;

    // Input
    cout << "Masukkan data kereta:\n";
    cout << "Kode: ";
    cin >> kereta.kode;
    cout << "Nama: ";
    cin.ignore();
    getline(cin, kereta.nama);
    cout << "Asal: ";
    getline(cin, kereta.asal);
    cout << "Tujuan: ";
    getline(cin, kereta.tujuan);
    cout << "Jadwal Keberangkatan (HH:MM): ";
    cin >> kereta.jadwal_keberangkatan;
    cout << "Jadwal Kedatangan (HH:MM): ";
    cin >> kereta.jadwal_kedatangan;
    cout << "Jumlah Gerbong: ";
    cin >> kereta.jumlah_gerbong;

    int pilihan;
    do {
        cout << "\n--- Menu ---\n";
        cout << "1. Tampilkan Informasi Kereta\n";
        cout << "2. Tambah Gerbong\n";
        cout << "3. Ubah Jadwal\n";
        cout << "4. Tambah Penumpang\n";
        cout << "5. Hapus Penumpang\n";
        cout << "6. Tampilkan Daftar Penumpang\n";
        cout << "0. Keluar\n";
        cout << "Pilih: ";
        cin >> pilihan;

        switch (pilihan) {
            case 1:
                tampilkanInformasi(kereta);
                break;
            case 2: {
                int jumlah;
                cout << "Masukkan jumlah gerbong yang akan ditambahkan: ";
                cin >> jumlah;
                tambahGerbong(kereta, jumlah);
                break;
            }
            case 3: {
                string keberangkatan, kedatangan;
                cout << "Masukkan jadwal keberangkatan baru (HH:MM): ";
                cin >> keberangkatan;
                cout << "Masukkan jadwal kedatangan baru (HH:MM): ";
                cin >> kedatangan;
                ubahJadwal(kereta, keberangkatan, kedatangan);
                break;
            }
            case 4: {
                string nama;
                cout << "Masukkan nama penumpang: ";
                cin.ignore();
                getline(cin, nama);
                tambahPenumpang(kereta, nama);
                break;
            }
            case 5: {
                string nama;
                cout << "Masukkan nama penumpang yang akan dihapus: ";
                cin.ignore();
                getline(cin, nama);
                hapusPenumpang(kereta, nama);
                break;
            }
            case 6:
                daftarPenumpang(kereta);
                break;
            case 0:
                cout << "Keluar dari program.\n";
                break;
            default:
                cout << "Pilihan tidak valid.\n";
        }
    } while (pilihan != 0);

    return 0;
}
