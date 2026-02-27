Ticket #002 – Brak adresu IP 

Opis zgłoszenia:
Użytkownik zgłasza całkowity brak dostępu do Internetu po uruchomieniu komputera. Ikona sieci wskazuje połączenie aktywne (Ethernet/Wi-Fi), jednak żadna strona internetowa nie otwiera się.

Środowisko:
- System: Windows 11
- Połączenie: Ethernet (VM – VirtualBox, NAT)
- Użytkownik bez uprawnień administracyjnych

Objawy:
- Brak dostępu do Internetu
- Połączenie sieciowe oznaczone jako „Połączono”
- Brak możliwości komunikacji z innymi urządzeniami w sieci

Diagnostyka:
1. Sprawdzenie stosu sieciowego:
   - `ping 127.0.0.1` – odpowiedź poprawna

2. Sprawdzenie konfiguracji adresu IP:
   - `ipconfig /all`
   - Adres IPv4: 169.254.x.x (APIPA)
   - Brak informacji o serwerze DHCP

3. Test łączności:
   - `ping 8.8.8.8` – brak odpowiedzi
   - `ping default gateway` – brak odpowiedzi
   (brak routingu poza hostem)

Wniosek z diagnostyki:
Komputer nie otrzymał adresu IP z serwera DHCP i przypisał adres APIPA (Automatic Private IP Addressing), co uniemożliwia komunikację sieciową.

Przyczyna:
Brak odpowiedzi serwera DHCP dla interfejsu sieciowego maszyny wirtualnej (nieaktywny adapter sieciowy / brak połączenia sieciowego w warstwie wirtualizacji).

Rozwiązanie:
- Weryfikacja konfiguracji sieci maszyny wirtualnej (VirtualBox)
- Włączenie adaptera sieciowego i ustawienie trybu NAT
- Restart interfejsu sieciowego w systemie
- Odnowienie dzierżawy DHCP:
  - `ipconfig /release`
  - `ipconfig /renew`

Weryfikacja:
- Przydzielenie poprawnego adresu IPv4 z zakresu prywatnego
- Obecny Default Gateway oraz DNS
- `ping 8.8.8.8` – odpowiedź poprawna
- `ping google.com` – odpowiedź poprawna

Status:
Zgłoszenie rozwiązane
