#include <iostream>
#include <string>
#include <queue>
using namespace std;
// Single Linked List
// Non-Circular Linked List
// Tipe Data
// Binary Search
// queue

// Node untuk linked list
struct DiamondNode
{
    int diamond;
    int price;
    DiamondNode *next;
};

// Deklarasi struktur data queue
struct QueueNode
{
    string id;
    string name;
    int diamondChoice;
    int paymentChoice;
    QueueNode *next;

    QueueNode(string id, string name, int diamondChoice, int paymentChoice)
        : id(id), name(name), diamondChoice(diamondChoice), paymentChoice(paymentChoice), next(nullptr)
    {
    }
};

class Queue
{
private:
    QueueNode *front;
    QueueNode *rear;

public:
    Queue() : front(nullptr), rear(nullptr) {}
    ~Queue()
    {
        while (!isEmpty())
        {
            dequeue();
        }
    }

    bool isEmpty() const
    {
        return front == nullptr;
    }

    void enqueue(string id, string name, int diamondChoice, int paymentChoice)
    {
        QueueNode *newNode = new QueueNode(id, name, diamondChoice, paymentChoice);
        if (isEmpty())
        {
            front = rear = newNode;
        }
        else
        {
            rear->next = newNode;
            rear = newNode;
        }
    }

    void dequeue()
    {
        if (!isEmpty())
        {
            QueueNode *temp = front;
            front = front->next;
            delete temp;
        }
    }

    // Anda juga bisa menambahkan fungsi-fungsi lain yang diperlukan untuk operasi queue
};

// Fungsi untuk menambahkan node ke linked list diamond
void addDiamond(DiamondNode *&head, int diamond, int price)
{
    DiamondNode *newNode = new DiamondNode;
    newNode->diamond = diamond;
    newNode->price = price;
    newNode->next = nullptr;

    if (head == nullptr)
    {
        head = newNode;
    }
    else
    {
        DiamondNode *curr = head;
        while (curr->next != nullptr)
        {
            curr = curr->next;
        }
        curr->next = newNode;
    }
}

// Fungsi untuk menampilkan daftar diamond
void displayDiamond(DiamondNode *head)
{
    DiamondNode *curr = head;
    while (curr != nullptr)
    {
        cout << "  " << curr->diamond << "\tdiamond = Rp. " << curr->price << endl;
        curr = curr->next;
    }
}

// Fungsi untuk membersihkan linked list diamond dari memory yang dialokasikan
void clearDiamond(DiamondNode *&head)
{
    while (head != nullptr)
    {
        DiamondNode *temp = head;
        head = head->next;
        delete temp;
    }
}
// Fungsi untuk memeriksa apakah jumlah diamond yang dimasukkan oleh user valid
bool isValidInput(DiamondNode *head, int input)
{
    DiamondNode *curr = head;
    while (curr != nullptr)
    {
        if (curr->diamond == input)
        {
            return true;
        }
        curr = curr->next;
    }
    return false;
}

bool binarySearch(DiamondNode *head, int input)
{
    DiamondNode *low = head;
    DiamondNode *high = nullptr;
    int len = 0;

    // Mencari panjang linked list
    while (low != nullptr)
    {
        len++;
        high = low;
        low = low->next;
    }

    low = head;

    // Algoritma binary search
    while (low != high && high->next != low)
    {
        int mid = (len + 1) / 2;
        DiamondNode *midNode = low;
        for (int i = 0; i < mid; i++)
        {
            midNode = midNode->next;
        }

        if (midNode->diamond == input)
        {
            return true;
        }
        else if (midNode->diamond > input)
        {
            high = midNode;
        }
        else
        {
            low = midNode->next;
        }
        len = len / 2;
    }

    if (low != nullptr && low->diamond == input)
    {
        return true;
    }

    return false;
}

int main()
{
    // Inisialisasi linked list diamond untuk setiap game
    DiamondNode *mlDiamonds = nullptr;
    addDiamond(mlDiamonds, 11, 1200);
    addDiamond(mlDiamonds, 23, 2500);
    addDiamond(mlDiamonds, 36, 3800);
    addDiamond(mlDiamonds, 58, 6000);
    addDiamond(mlDiamonds, 74, 7600);
    addDiamond(mlDiamonds, 116, 12000);
    addDiamond(mlDiamonds, 163, 16800);
    addDiamond(mlDiamonds, 219, 22000);
    addDiamond(mlDiamonds, 366, 36000);
    addDiamond(mlDiamonds, 562, 55000);
    addDiamond(mlDiamonds, 1183, 115000);
    addDiamond(mlDiamonds, 2375, 230000);
    addDiamond(mlDiamonds, 4812, 460000);
    addDiamond(mlDiamonds, 9865, 920000);

    DiamondNode *ffDiamonds = nullptr;
    addDiamond(ffDiamonds, 50, 10000);
    addDiamond(ffDiamonds, 100, 20000);
    addDiamond(ffDiamonds, 310, 50000);
    addDiamond(ffDiamonds, 520, 80000);
    addDiamond(ffDiamonds, 1065, 160000);
    addDiamond(ffDiamonds, 2200, 320000);
    addDiamond(ffDiamonds, 5600, 800000);
    addDiamond(ffDiamonds, 11500, 1600000);
    addDiamond(ffDiamonds, 23500, 3200000);

    DiamondNode *genshinPrimogem = nullptr;
    addDiamond(genshinPrimogem, 60, 10000);
    addDiamond(genshinPrimogem, 300, 50000);
    addDiamond(genshinPrimogem, 980, 160000);
    addDiamond(genshinPrimogem, 1980, 320000);
    addDiamond(genshinPrimogem, 3280, 530000);
    addDiamond(genshinPrimogem, 6480, 1050000);
    addDiamond(genshinPrimogem, 12880, 2080000);

    DiamondNode *aovVoucher = nullptr;
    addDiamond(aovVoucher, 22, 6000);
    addDiamond(aovVoucher, 44, 12000);
    addDiamond(aovVoucher, 69, 18000);
    addDiamond(aovVoucher, 140, 35000);
    addDiamond(aovVoucher, 220, 50000);
    addDiamond(aovVoucher, 550, 125000);
    addDiamond(aovVoucher, 1200, 270000);
    addDiamond(aovVoucher, 2000, 450000);

    DiamondNode *pubgUC = nullptr;
    addDiamond(pubgUC, 60, 12000);
    addDiamond(pubgUC, 325, 55000);
    addDiamond(pubgUC, 660, 115000);
    addDiamond(pubgUC, 1800, 275000);
    addDiamond(pubgUC, 3850, 550000);
    addDiamond(pubgUC, 8100, 1100000);

    // Queue untuk menyimpan pesanan
    Queue orderQueue;

// Menampilkan menu selamat datang
gamemenu:
    cout << "=========================================" << endl;
    cout << "\ttop up game Ngkene Bae\t" << endl;
    cout << "=========================================" << endl;
    cout << "1. Mobile Legend" << endl;
    cout << "2. Free Fire" << endl;
    cout << "3. Genshin Impact" << endl;
    cout << "4. Arena of Valor" << endl;
    cout << "5. PUBG Mobile" << endl;
    cout << "pilih : ";
    int choice;
    cin >> choice;

    // Memproses pilihan pengguna
    switch (choice)
    {
    case 1:
    {
        cout << "\n-----------------------------" << endl;
        cout << "\tMobile Legend\t" << endl;
        cout << "-----------------------------" << endl;
        displayDiamond(mlDiamonds);
        cout << "-----------------------------" << endl;
        break;
    }
    case 2:
    {
        cout << "\n-----------------------------" << endl;
        cout << "\tFree Fire\t" << endl;
        cout << "-----------------------------" << endl;
        displayDiamond(ffDiamonds);
        cout << "-----------------------------" << endl;
        break;
    }
    case 3:
    {
        cout << "\n-----------------------------" << endl;
        cout << "\tGenshin Impact\t" << endl;
        cout << "-----------------------------" << endl;
        displayDiamond(genshinPrimogem);
        cout << "-----------------------------" << endl;
        break;
    }
    case 4:
    {
        cout << "\n-----------------------------" << endl;
        cout << "\tArena of Valor\t" << endl;
        cout << "-----------------------------" << endl;
        displayDiamond(aovVoucher);
        cout << "-----------------------------" << endl;
        break;
    }
    case 5:
    {
        cout << "\n-----------------------------" << endl;
        cout << "\tPUBG Mobile\t" << endl;
        cout << "-----------------------------" << endl;
        displayDiamond(pubgUC);
        cout << "-----------------------------" << endl;
        break;
    }
    default:
    {
        cout << "\nPilihan Anda tidak valid." << endl;
        return 0;
    }
    }

    // Meminta pengguna untuk memilih jumlah diamond yang ingin dibeli
    int diamondChoice;
    bool validInput = false;
    while (!validInput)
    {
        cout << "Pilih jumlah diamond: ";
        cin >> diamondChoice;
        validInput = binarySearch(mlDiamonds, diamondChoice) || binarySearch(ffDiamonds, diamondChoice) || binarySearch(genshinPrimogem, diamondChoice) || binarySearch(aovVoucher, diamondChoice) || binarySearch(pubgUC, diamondChoice);
        if (!validInput)
        {
            cout << "\nPermintaan tidak valid! Mohon masukkan jumlah yang sesuai." << endl;
        }
    }
    // Meminta pengguna untuk memasukkan ID game dan nama
    string id, name;
    cout << "\n-----------------------------" << endl;
    cout << "\tDetail Akun\t" << endl;
    cout << "-----------------------------" << endl;
    cout << "User ID: ";
    cin >> id;
    cout << "Username: ";
    cin >> name;

    // Meminta pengguna untuk memilih metode pembayaran
    cout << "\n---------------------------------" << endl;
    cout << "\tMetode pembayaran\t" << endl;
    cout << "---------------------------------" << endl;
    cout << "1. Dana" << endl;
    cout << "2. OVO" << endl;
    cout << "3. Gopay" << endl;
    cout << "4. Shopee Pay" << endl;
    cout << "5. Link Aja" << endl;
    cout << "6. Batalkan Pesanan" << endl;
    cout << "Pilih : ";
    int paymentChoice;
    cin >> paymentChoice;

    // Memproses pilihan pengguna
    switch (paymentChoice)
    {
    case 1:
    {
        // Meminta pengguna untuk mengisi nomor telepon dan nominal harga
        string phoneNumber;
        int price;
        cout << "Masukkan nomor telepon: ";
        cin >> phoneNumber;
        cout << "Masukan Nominal Harga: ";
        cin >> price;
        cout << "Pesanan Anda akan segera diproses." << endl;
        cout << "\n-----------------------------" << endl;
        cout << "\tDetail Pesanan\t" << endl;
        cout << "-----------------------------" << endl;
        cout << "Jumlah Pesanan: " << diamondChoice << endl;
        cout << "Metode pembayaran: Dana" << endl;
        cout << "Total Pembayaran: " << price << endl;
        cout << "User ID: " << id << endl;
        cout << "Username: " << name << endl;
        orderQueue.enqueue(id, name, diamondChoice, paymentChoice);
        break;
    }
    case 2:
    {
        // Meminta pengguna untuk mengisi nomor telepon dan nominal harga
        string phoneNumber;
        int price;
        cout << "Masukkan nomor telepon: ";
        cin >> phoneNumber;
        cout << "Masukan Nominal Harga: ";
        cin >> price;
        cout << "Pesanan Anda akan segera diproses." << endl;
        cout << "\n-----------------------------" << endl;
        cout << "\tDetail Pesanan\t" << endl;
        cout << "-----------------------------" << endl;
        cout << "Jumlah Pesanan: " << diamondChoice << endl;
        cout << "Metode pembayaran: OVO" << endl;
        cout << "Total Pembayaran: " << price << endl;
        cout << "User ID: " << id << endl;
        cout << "Username: " << name << endl;
        orderQueue.enqueue(id, name, diamondChoice, paymentChoice);
        break;
    }
    case 3:
    {
        // Meminta pengguna untuk mengisi nomor telepon dan nominal harga
        string phoneNumber;
        int price;
        cout << "Masukkan nomor telepon: ";
        cin >> phoneNumber;
        cout << "Masukan Nominal Harga: ";
        cin >> price;
        cout << "Pesanan Anda akan segera diproses." << endl;
        cout << "\n-----------------------------" << endl;
        cout << "\tDetail Pesanan\t" << endl;
        cout << "-----------------------------" << endl;
        cout << "Jumlah Pesanan: " << diamondChoice << endl;
        cout << "Metode pembayaran: Gopay" << endl;
        cout << "Total Pembayaran: " << price << endl;
        cout << "User ID: " << id << endl;
        cout << "Username: " << name << endl;
        orderQueue.enqueue(id, name, diamondChoice, paymentChoice);
        break;
    }
    case 4:
    {
        // Meminta pengguna untuk mengisi nomor telepon dan nominal harga
        string phoneNumber;
        int price;
        cout << "Masukkan nomor telepon: ";
        cin >> phoneNumber;
        cout << "Masukan Nominal Harga: ";
        cin >> price;
        cout << "Pesanan Anda akan segera diproses." << endl;
        cout << "\n-----------------------------" << endl;
        cout << "\tDetail Pesanan\t" << endl;
        cout << "-----------------------------" << endl;
        cout << "Jumlah Pesanan: " << diamondChoice << endl;
        cout << "Metode pembayaran: Shopee Pay" << endl;
        cout << "Total Pembayaran: " << price << endl;
        cout << "User ID: " << id << endl;
        cout << "Username: " << name << endl;
        orderQueue.enqueue(id, name, diamondChoice, paymentChoice);
        break;
    }
    case 5:
    {
        // Meminta pengguna untuk mengisi nomor telepon dan nominal harga
        string phoneNumber;
        int price;
        cout << "Masukkan nomor telepon: ";
        cin >> phoneNumber;
        cout << "Masukan Nominal Harga: ";
        cin >> price;
        cout << "Pesanan Anda akan segera diproses." << endl;
        cout << "\n-----------------------------" << endl;
        cout << "\tDetail Pesanan\t" << endl;
        cout << "-----------------------------" << endl;
        cout << "Jumlah Pesanan: " << diamondChoice << endl;
        cout << "Metode pembayaran: Link Aja" << endl;
        cout << "Total Pembayaran: " << price << endl;
        cout << "User ID: " << id << endl;
        cout << "Username: " << name << endl;
        orderQueue.enqueue(id, name, diamondChoice, paymentChoice);
        break;
    }
    case 6:
    {
        cout << "Pesanan Anda telah dibatalkan." << endl;
        goto gamemenu;
        break;
    }
    default:
    {
        cout << "Pilihan Anda tidak valid." << endl;
        return 0;
    }
    }
    return 0;
}
