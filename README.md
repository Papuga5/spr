#spr123321

# 1p-Napisz skrypt co wygeneruje 20 liczb pierwszych w pliku tekstowym ppp.txt. 



def czy_pierwsza(liczba):
    if liczba < 2:
        return False
    for i in range(2, int(liczba ** 0.5) + 1):
        if liczba % i == 0:
            return False
    return True

def generuj_liczby_pierwsze(ile):
    liczby_pierwsze = []
    aktualna_liczba = 2
    while len(liczby_pierwsze) < ile:
        if czy_pierwsza(aktualna_liczba):
            liczby_pierwsze.append(aktualna_liczba)
        aktualna_liczba += 1
    return liczby_pierwsze

if __name__ == "__main__":
    liczby_pierwsze = generuj_liczby_pierwsze(20)
    with open("ppp.txt", "w") as plik:
        plik.write("Wygenerowane liczby pierwsze:\n")
        for liczba in liczby_pierwsze:
            plik.write(str(liczba) + "\n")
            
    print("Liczby pierwsze zostały zapisane do pliku 'ppp.txt'.")



# 1p-Napisz skrypt co wygeneruje 20 liczb ciągu fibonacciego w pliku tekstowym fff.txt


def genrate_text(file_name: str, content: str):
    file_name = file_name + ".txt"
    with open(file_name, "w") as text_file:
        text_file.write(content)

def fibonacci_sequence(n):
    el_1 = 1
    el_2 = 1
    nex_el = 0
    text = f"{el_1} {el_2}"
    for _ in range(n - 2):  
        nex_el = el_1 + el_2
        text += f" {nex_el}"
        el_1 = el_2
        el_2 = nex_el
    return text

text = fibonacci_sequence(20)
genrate_text("fff", text)
print("Wygenerowane liczby ciągu Fibonacciego zostały zapisane do pliku 'fff.txt'.")






# # # # # # # # # Wersja 1

# Napisz skrypt co przepisze liczby pierwsze do zzz.txt jeśli znajdują się one w obu plikach  ppp.txt / fff.txt

def czy_pierwsza(liczba):
    if liczba < 2:
        return False
    for i in range(2, int(liczba ** 0.5) + 1):
        if liczba % i == 0:
            return False
    return True

def wczytaj_liczby_pierwsze(file_name):
    liczby_pierwsze = set()
    with open(file_name, "r") as plik:
        next(plik)  # Pominięcie pierwszej linii z opisem
        for linia in plik:
            liczba = int(linia.strip())
            liczby_pierwsze.add(liczba)
    return liczby_pierwsze

def zapisz_do_zzz(liczby_pierwsze, file_name):
    with open(file_name, "w") as zzz_file:
        for liczba in sorted(liczby_pierwsze):
            zzz_file.write(str(liczba) + "\n")

if __name__ == "__main__":
    liczby_pierwsze_z_ppp = wczytaj_liczby_pierwsze("ppp.txt")
    liczby_z_fff = set()
    with open("fff.txt", "r") as fff_file:
        for linia in fff_file:
            liczby_z_fff.update(map(int, linia.strip().split()))

    wspolne_liczby_pierwsze = liczby_pierwsze_z_ppp.intersection(liczby_z_fff)
    zapisz_do_zzz(wspolne_liczby_pierwsze, "zzz.txt")
    print("Wspólne liczby pierwsze zostały zapisane do pliku 'zzz.txt'.")




# 1p-Napisz skrypt co zmieni wszystkie z pliku zzz.txt na liczby binarne 

def dec_to_bin(liczba):
    return bin(liczba)[2:]  # Konwersja na liczbę binarną i usunięcie prefixu '0b'.

def zmien_na_binarny(plik_wejsciowy, plik_wyjsciowy):
    with open(plik_wejsciowy, "r") as plik_wej:
        liczby_dec = [int(linia.strip()) for linia in plik_wej if linia.strip()]  # Wczytanie i konwersja na int.

    liczby_bin = [dec_to_bin(liczba) for liczba in liczby_dec]  # Konwersja na liczby binarne.

    with open(plik_wyjsciowy, "w") as plik_wyj:
        for liczba_bin in liczby_bin:
            plik_wyj.write(liczba_bin + "\n")  # Zapisanie liczby binarnej do pliku.

if __name__ == "__main__":
    zmien_na_binarny("zzz.txt", "binarny_zzz.txt")
    print("Liczby z pliku 'zzz.txt' zostały przekonwertowane na liczby binarne i zapisane do pliku 'binarny_zzz.txt'.")


# # # # # # Wersja 2


# 2p-Napisz skrypt co  przepisze  liczby z pliku fff.txt + rozłoży liczby na czynniki pierwsze i zapisze je z pliku zzz.txt.
# 100 2 2 5 5 
# 8 2 2 2
# 20 2 2 5

def czy_pierwsza(liczba):
    if liczba < 2:
        return False
    for i in range(2, int(liczba ** 0.5) + 1):
        if liczba % i == 0:
            return False
    return True

def rozloz_na_czynniki_pierwsze(liczba):
    czynniki = []
    dzielnik = 2
    while liczba > 1:
        if liczba % dzielnik == 0:
            czynniki.append(dzielnik)
            liczba //= dzielnik
        else:
            dzielnik += 1
    return czynniki

def przepisz_i_rozloz(plik_wejsciowy, plik_wyjsciowy):
    try:
        with open(plik_wejsciowy, "r") as plik_wej:
            liczby = [int(l) for linia in plik_wej for l in linia.strip().split() if l.strip()]

        with open(plik_wyjsciowy, "w") as plik_wyj:
            for liczba in liczby:
                czynniki = rozloz_na_czynniki_pierwsze(liczba)
                plik_wyj.write(f"Liczba: {liczba}, Czynniki pierwsze: {', '.join(map(str, czynniki))}\n")
    
    except FileNotFoundError:
        print(f"Plik {plik_wejsciowy} nie został znaleziony.")
    except Exception as e:
        print(f"Wystąpił błąd: {e}")

if __name__ == "__main__":
    przepisz_i_rozloz("fff.txt", "zzz.txt")
    print("Operacja zakończona.")





# 1p-Napisz skrypt co powie ile występuje liczb pierwszych (wszystkie liczby pierwsze) w pliku zzz.txt. 

def czy_pierwsza(liczba):
    if liczba < 2:
        return False
    for i in range(2, int(liczba ** 0.5) + 1):
        if liczba % i == 0:
            return False
    return True

def policz_liczby_pierwsze(plik_wejsciowy):
    liczby_pierwsze = 0
    with open(plik_wejsciowy, "r") as plik:
        for linia in plik:
            for liczba in linia.strip().split():
                try:
                    if czy_pierwsza(int(liczba)):
                        liczby_pierwsze += 1
                except ValueError:
                    pass  # Ignoruj linie, które nie zawierają liczb całkowitych
    return liczby_pierwsze

if __name__ == "__main__":
    plik_wejsciowy = "zzz.txt"
    liczba_liczb_pierwszych = policz_liczby_pierwsze(plik_wejsciowy)
    print(f"W pliku '{plik_wejsciowy}' znajduje się {liczba_liczb_pierwszych} liczb pierwszych.")


