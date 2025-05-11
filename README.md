# Systemy czasu rzeczywistego - Model Automatu do Gorących Napojów w języku AADL

# Autor:
- Tomasz Madeja, tomaszmadeja@student.agh.edu.pl
- Karol Kowalczyk, bolek@student.agh.edu.pl

# Opis projektu

Projekt "Automat do Gorących Napojów" realizowany jest w języku AADL i ma na celu stworzenie uproszczonego modelu systemu sterowania dla maszyny vendingowej. System skupia się na podstawowych funkcjach czasu rzeczywistego, takich jak obsługa użytkownika, kontrola przygotowania napoju oraz monitorowanie stanu urządzenia. Model został zaprojektowany z myślą o przejrzystości i ograniczeniu liczby komponentów do niezbędnego minimum, aby zademonstrować kluczowe aspekty modelowania systemów w AADL.

# Funkcjonalności systemu:

- Wybór napoju przez użytkownika.
- Symulacja procesu płatności.
- Sterowanie dozowaniem składników i wydawaniem kubka.
- Kontrola procesu podgrzewania wody.
- Wyświetlanie podstawowych statusów i komunikatów dla użytkownika.
- Monitorowanie kluczowych parametrów (np. temperatura wody, uproszczony stan zapasów).
- Możliwość wysyłania podstawowych informacji o stanie automatu przez sieć (uproszczona symulacja).

# Planowane komponenty projektu:

### Pakiet
- `VendingMachine_Pkg` – główny pakiet grupujący wszystkie elementy modelu automatu.

### System
- `VendingMachine_Sys` – główny komponent systemowy, integrujący podsystemy automatu.

### Procesor
- `Control_Cpu` – abstrakcyjny procesor wykonujący logikę sterowania automatem.

### Pamięć
- `Control_Mem` – pamięć operacyjna dla procesora i danych systemu.

### Magistrala
- `System_Bus` – pojedyncza magistrala systemowa do komunikacji między kluczowymi komponentami (procesor, pamięć, urządzenia).

### Dane
- `Machine_Operational_Data` – zagregowane dane operacyjne, obejmujące wybór użytkownika, odczyty z czujników (temperatura, poziomy), status maszyny oraz komendy dla urządzeń wykonawczych.

### Proces
- `Control_Logic_Process` – proces odpowiedzialny za główną logikę decyzyjną automatu.
- `IO_Handling_Process` – proces zarządzający interakcjami z urządzeniami wejścia/wyjścia oraz komunikacją sieciową.

### Wątki
- `Main_Coordinator_Thread` (zawarty w `Control_Logic_Process`) – główny wątek koordynujący, zarządzający stanem automatu i podejmowaniem decyzji.
- `Device_Interface_Thread` (zawarty w `IO_Handling_Process`) – wątek obsługujący komunikację z fizycznymi czujnikami i urządzeniami wykonawczymi.
- `Network_Interface_Thread` (zawarty w `IO_Handling_Process`) – wątek odpowiedzialny za uproszczoną komunikację sieciową (np. wysyłanie statusu).

### Urządzenia
- `User_Panel_Device` – zintegrowane urządzenie wejścia/wyjścia dla użytkownika (przyciski wyboru, prosty wyświetlacz statusu).
- `Heating_Element_Device` – urządzenie wykonawcze odpowiedzialne za podgrzewanie wody.
- `Multi_Dispenser_Device` – zintegrowane urządzenie wykonawcze do dozowania składników napoju oraz wydawania kubka.
- `Network_Adapter_Device` – urządzenie reprezentujące fizyczny interfejs sieciowy.

# Diagram Systemu

Poniżej przedstawiono diagram komponentów systemu automatu do gorących napojów.

![Diagram automatu do napojów](vending_machine_diagram.jpg)


# Bibliografia:

1.  SAE International. *AS5506D: Architecture Analysis & Design Language (AADL)*. Kwiecień 2022. Dostępne: `https://www.sae.org/standards/content/as5506/`
2.  Feiler, P. H., Gluch, D. P., & Hudak, J. J. *Model-Based Engineering with AADL: An Introduction to the SAE Architecture Analysis & Design Language*. Addison-Wesley Professional, Wrzesień 2012. Dostępne: `https://www.amazon.com/Model-Based-Engineering-AADL-Introduction-Architecture/dp/0134208897`
3.  Software Engineering Institute, Carnegie Mellon University. *Architecture Analysis and Design Language (AADL)*. Dostępne: `https://insights.sei.cmu.edu/projects/architecture-analysis-and-design-language-aadl/`
4.  *EP1321908A2: Vending machine control system*. Zgłoszony 18 grudnia 2002. Dostępne: `https://patents.google.com/patent/EP1321908A2/en`
