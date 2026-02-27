Ticket #001 – Przerywane połączenie z Internetem (Windows 11)

Opis zgłoszenia:
Użytkownik zgłasza, że po uruchomieniu komputera Internet działa poprawnie, jednak po kilku minutach przestają otwierać się strony internetowe. Połączenie Wi-Fi/LAN pozostaje aktywne.

Środowisko:
- System: Windows 11
- Połączenie sieciowe: Ethernet (VM – VirtualBox, NAT)
- Użytkownik bez uprawnień administracyjnych

Objawy:
- Brak dostępu do stron internetowych po nazwie domenowej
- Ikona sieci wskazuje połączenie aktywne
- Problem występuje nieregularnie

Diagnostyka:
1. Sprawdzenie stosu sieciowego:
   - `ping 127.0.0.1` – odpowiedź poprawna
   (system operacyjny działa prawidłowo)

2. Sprawdzenie konfiguracji IP:
   - `ipconfig /all`
   - Adres IPv4 przypisany poprawnie
   - Default Gateway obecny
   - Serwer DNS ustawiony statycznie na adres spoza zakresu operatora

3. Test połączenia bez DNS:
   - `ping 8.8.8.8` – odpowiedź poprawna
   (połączenie z Internetem dostępne)

4. Test rozwiązywania nazw:
   - `ping google.com` – brak odpowiedzi
   - `nslookup google.com` – timeout

Wniosek z diagnostyki:
Połączenie sieciowe oraz routing działają poprawnie. Problem dotyczy wyłącznie rozwiązywania nazw domenowych (DNS).

Przyczyna:
Nieprawidłowo skonfigurowany serwer DNS ustawiony ręcznie, powodujący okresowe przerwy w rozwiązywaniu nazw.

Rozwiązanie:
- Przywrócenie automatycznego pobierania adresów DNS (DHCP)
- Alternatywnie ustawienie publicznych serwerów DNS (1.1.1.1, 8.8.8.8)
- Restart interfejsu sieciowego

Weryfikacja:
- `ping google.com` – odpowiedź poprawna
- `nslookup google.com` – poprawne tłumaczenie adresu
- Brak ponownego wystąpienia problemu

Status:
Zgłoszenie rozwiązane
