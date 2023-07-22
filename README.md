import java.util.Scanner;

// Kelas induk Buku
class Buku {
    protected String judul;
    protected double hargaBeli;
    protected double hargaJual;
    protected int jumlahStok;

    public Buku(String judul, double hargaBeli, double hargaJual, int jumlahStok) {
        this.judul = judul;
        this.hargaBeli = hargaBeli;
        this.hargaJual = hargaJual;
        this.jumlahStok = jumlahStok;
    }

    // Method untuk menambah stok
    public void tambahStok(int jumlah) {
        jumlahStok += jumlah;
    }

    // Method untuk mengurangi stok
    public void kurangiStok(int jumlah) {
        jumlahStok -= jumlah;
        if (jumlahStok <= 0) {
            System.out.println("Stok " + judul + " sudah mencapai nol!");
        }
    }

    // Method untuk menampilkan informasi buku
    public void tampilkanInfo() {
        System.out.println("Judul: " + judul);
        System.out.println("Harga Beli: " + hargaBeli);
        System.out.println("Harga Jual: " + hargaJual);
        System.out.println("Stok: " + jumlahStok);
    }
}

// Kelas turunan BukuFiksi
class BukuFiksi extends Buku {
    public BukuFiksi(String judul, double hargaBeli, double hargaJual, int jumlahStok) {
        super(judul, hargaBeli, hargaJual, jumlahStok);
    }
}

// Kelas turunan BukuNonFiksi
class BukuNonFiksi extends Buku {
    public BukuNonFiksi(String judul, double hargaBeli, double hargaJual, int jumlahStok) {
        super(judul, hargaBeli, hargaJual, jumlahStok);
    }
}

// Kelas turunan Majalah
class Majalah extends Buku {
    private int nomorEdisi;

    public Majalah(String judul, double hargaBeli, double hargaJual, int jumlahStok, int nomorEdisi) {
        super(judul, hargaBeli, hargaJual, jumlahStok);
        this.nomorEdisi = nomorEdisi;
    }

    // Method untuk menampilkan informasi majalah
    @Override
    public void tampilkanInfo() {
        super.tampilkanInfo();
        System.out.println("Nomor Edisi: " + nomorEdisi);
    }
}

public class ManajemenPenjualanBuku {
    public static void main(String[] args) {
        // Inisialisasi modal awal dan modal berjalan
        double modalAwal = 1000.0;
        double modalBerjalan = modalAwal;

        // Inisialisasi beberapa contoh buku dan majalah
        BukuFiksi bukuFiksi = new BukuFiksi("Buku Fiksi 1", 10.0, 20.0, 50);
        BukuNonFiksi bukuNonFiksi = new BukuNonFiksi("Buku Non Fiksi 1", 15.0, 25.0, 30);
        Majalah majalah = new Majalah("Majalah 1", 5.0, 10.0, 20, 3);

        Scanner scanner = new Scanner(System.in);
        int choice;

        System.out.println("Sistem Penjualan Buku");
        System.out.print("By: <Nama Anda>, <NIM Anda>\n");

        // Loop program
        do {
            System.out.println("\nSilakan pilih menu:");
            System.out.println("1) Beli Buku 2) Jual Buku 3) Lihat Stok Buku 4) Lihat Laporan Keuangan 5) Exit");
            System.out.print("Pilihan Menu: ");
            choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    // Lakukan pembelian dan kurangi modal berjalan
                    System.out.println("Pilih jenis buku:");
                    System.out.println("1) Buku Fiksi 2) Buku Non Fiksi 3) Majalah");
                    System.out.print("Pilihan: ");
                    int jenisBuku = scanner.nextInt();
                    int jumlahBeli;

                    switch (jenisBuku) {
                        case 1:
                            bukuFiksi.tampilkanInfo();
                            System.out.print("Jumlah buku yang dibeli: ");
                            jumlahBeli = scanner.nextInt();
                            if (modalBerjalan >= bukuFiksi.hargaBeli * jumlahBeli) {
                                modalBerjalan -= (bukuFiksi.hargaBeli * jumlahBeli);
                                bukuFiksi.tambahStok(jumlahBeli);
                                System.out.println("Pembelian berhasil!");
                            } else {
                                System.out.println("Uang tidak cukup untuk melakukan pembelian.");
                            }
                            break;
                        case 2:
                            bukuNonFiksi.tampilkanInfo();
                            System.out.print("Jumlah buku yang dibeli: ");
                            jumlahBeli = scanner.nextInt();
                            if (modalBerjalan >= bukuNonFiksi.hargaBeli * jumlahBeli) {
                                modalBerjalan -= (bukuNonFiksi.hargaBeli * jumlahBeli);
                                bukuNonFiksi.tambahStok(jumlahBeli);
                                System.out.println("Pembelian berhasil!");
                            } else {
                                System.out.println("Uang tidak cukup untuk melakukan pembelian.");
                            }
                            break;
                        case 3:
                            majalah.tampilkanInfo();
                            System.out.print("Jumlah majalah yang dibeli: ");
                            jumlahBeli = scanner.nextInt();
                            if (modalBerjalan >= majalah.hargaBeli * jumlahBeli) {
                                modalBerjalan -= (majalah.hargaBeli * jumlahBeli);
                                majalah.tambahStok(jumlahBeli);
                                System.out.println("Pembelian berhasil!");
                            } else {
                                System.out.println("Uang tidak cukup untuk melakukan pembelian.");
                            }
                            break;
                        default:
                            System.out.println("Pilihan tidak valid.");
                    }
                    break;
                case 2:
                    // Lakukan penjualan dan tambahkan keuntungan ke modal berjalan
                    System.out.println("Pilih jenis buku:");
                    System.out.println("1) Buku Fiksi 2) Buku Non Fiksi 3) Majalah");
                    System.out.print("Pilihan: ");
                    jenisBuku = scanner.nextInt();
                    int jumlahJual;

                    switch (jenisBuku) {
                        case 1:
                            bukuFiksi.tampilkanInfo();
                            System.out.print("Jumlah buku yang dijual: ");
                            jumlahJual = scanner.nextInt();
                            if (jumlahJual <= bukuFiksi.jumlahStok) {
                                modalBerjalan += (bukuFiksi.hargaJual * jumlahJual);
                                bukuFiksi.kurangiStok(jumlahJual);
                                System.out.println("Penjualan berhasil!");
                            } else {
                                System.out.println("Stok tidak mencukupi untuk melakukan penjualan.");
                            }
                            break;
                        case 2:
                            bukuNonFiksi.tampilkanInfo();
                            System.out.print("Jumlah buku yang dijual: ");
                            jumlahJual = scanner.nextInt();
                            if (jumlahJual <= bukuNonFiksi.jumlahStok) {
                                modalBerjalan += (bukuNonFiksi.hargaJual * jumlahJual);
                                bukuNonFiksi.kurangiStok(jumlahJual);
                                System.out.println("Penjualan berhasil!");
                            } else {
                                System.out.println("Stok tidak mencukupi untuk melakukan penjualan.");
                            }
                            break;
                        case 3:
                            majalah.tampilkanInfo();
                            System.out.print("Jumlah majalah yang dijual: ");
                            jumlahJual = scanner.nextInt();
                            if (jumlahJual <= majalah.jumlahStok) {
                                modalBerjalan += (majalah.hargaJual * jumlahJual);
                                majalah.kurangiStok(jumlahJual);
                                System.out.println("Penjualan berhasil!");
                            } else {
                                System.out.println("Stok tidak mencukupi untuk melakukan penjualan.");
                            }
                            break;
                        default:
                            System.out.println("Pilihan tidak valid.");
                    }
                    break;
                case 3:
                    // Menampilkan stok buku untuk tiap jenis
                    System.out.println("Stok Buku Fiksi:");
                    bukuFiksi.tampilkanInfo();
                    System.out.println("Stok Buku Non Fiksi:");
                    bukuNonFiksi.tampilkanInfo();
                    System.out.println("Stok Majalah:");
                    majalah.tampilkanInfo();
                    break;
                case 4:
                    // Menampilkan laporan berisi modal awal dan modal berjalan
                    System.out.println("Modal Awal: " + modalAwal);
                    System.out.println("Modal Berjalan: " + modalBerjalan);
                    break;
                case 5:
                    System.out.println("Program Selesai");
                    break;
                default:
                    System.out.println("Pilihan tidak valid.");
            }
        } while (choice != 5);

        scanner.close();
    }
}
