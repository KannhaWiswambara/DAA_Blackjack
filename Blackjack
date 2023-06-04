# Pengacakan dengan fisher-yates shuffle
import random
def acak_kartu(deck, n):
    if n == 0:
        return deck
    index = random.randint(0, n)
    deck[n], deck[index] = deck[index], deck[n]
    acak_kartu(deck, n - 1)

# Fungsi untuk memberikan opening card ke pemain
def opening_card(deck):
    players = [[] for _ in range(4)]
    for _ in range(2):
        for i in range(4):
            card = deck.pop()
            players[i].append(card)
    return players

# Fungsi untuk menunjukan kartu pemain
def display_kartu(players):
    for i, player in enumerate(players):
        print(f"Pemain {i+1}: {player}")

# Fungsi untuk menambahkan kartu ke pemain
def tambah_kartu(deck, player):
    if len(deck) > 0:
        card = deck.pop()
        player.append(card)
        print(f"Kartu {card} ditambahkan kepada Pemain {player}")

# Fungsi untuk menyatakan nilai kartu selain angka
def nilai_kartu(card):
    rank = card[0]
    if rank == 'As':
        return 1
    elif rank == 'J':
        return 11
    elif rank == 'Q':
        return 12
    elif rank == 'K':
        return 13
    else:
        return int(rank)

# Fungsi untuk menghitung nilai kartu pemain
def hitung_nilai_kartu(players):
    max_total = 0
    best_combination = []

    for i in range(len(players[0])):
        for j in range(len(players[1])):
            for k in range(len(players[2])):
                for l in range(len(players[3])):
                    total = sum([nilai_kartu(players[0][i]),
                                 nilai_kartu(players[1][j]),
                                 nilai_kartu(players[2][k]),
                                 nilai_kartu(players[3][l])])

                    if total > max_total:
                        max_total = total
                        best_combination = [players[0][i], players[1][j], players[2][k], players[3][l]]

    return max_total, best_combination

#fungsi untuk membandingkan nilai kartu pemain
def bandingkan_players(players):
    max_total = 0
    best_player = None

    for i, player in enumerate(players):
        total = sum([nilai_kartu(card) for card in player])

        if total > max_total:
            max_total = total
            best_player = i + 1
    return best_player

# Fungsi penentuan pemenang
def tentukan_pemenang(players):
    max_total = 0
    winner = None
    for i, player in enumerate(players):
        total = sum([nilai_kartu(card) for card in player])

        if total <= 21:
            if total > max_total:
                max_total = total
                winner = i + 1
            elif total == max_total:
                brute_force_total = hitung_nilai_kartu([players[i], players[winner-1]])
                if brute_force_total == total:
                    continue
                elif brute_force_total > total:
                    winner = i + 1
    return winner

# Daftar kartu remi
suits = ['Hati', 'Sekop', 'Keriting', 'Wajik']
ranks = ['As', '2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K']

# Membangun deck kartu remi
deck = [(rank, suit) for rank in ranks for suit in suits]

# Mengacak kartu menggunakan algoritma Fisher-Yates
acak_kartu(deck, len(deck) - 1)

# Membagikan kartu awal kepada empat pemain
players = opening_card(deck)

# Menampilkan hasil pembagian kartu
display_kartu(players)

# Looping untuk pemain menambahkan kartu atau melakukan stand
while True:
    choice = input("Pemain mana yang ingin menambahkan kartu? (1-4) atau 'stand' untuk keluar: ")
    if choice == 'stand':
        break
    try:
        player_index = int(choice) - 1
        if player_index >= 0 and player_index < 4:
            tambah_kartu(deck, players[player_index])
            display_kartu(players)
        else:
            print("Pemain tidak valid. Silakan pilih pemain antara 1 hingga 4.")
    except ValueError:
        print("Input tidak valid. Silakan masukkan nomor pemain antara 1 hingga 4 atau 'stand'.")

# Menampilkan total nilai kartu dari semua pemain
for i, player in enumerate(players):
    print(f"Total nilai kartu Pemain {i+1}: {sum([nilai_kartu(card) for card in player])}")

# Menentukan pemenang permainan
winner = tentukan_pemenang(players)
if winner is not None:
    print(f"Pemenang dari permainan adalah : Pemain {winner}")
else:
    print("Tidak ada pemenang semua pemain melebihi nilai 21")

print("Permainan selesai.")
