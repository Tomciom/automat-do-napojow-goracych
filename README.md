# Systemy czasu rzeczywistego - Model Automatu do Gorących Napojów w języku AADL

# Autor:
- Tomasz Madeja, tomaszmadeja@student.agh.edu.pl
- Karol Kowalczyk, bolek@student.agh.edu.pl

# Opis projektu

Projekt "Automat do Gorących Napojów" realizowany jest w języku AADL i ma na celu stworzenie modelu systemu sterowania dla maszyny vendingowej. System skupia się na podstawowych funkcjach czasu rzeczywistego, takich jak obsługa użytkownika, kontrola przygotowania napoju, monitorowanie stanu urządzenia oraz zapewnienie podstawowych mechanizmów bezpieczeństwa. Model został zaprojektowany z myślą o przejrzystości, demonstrując kluczowe aspekty modelowania systemów w AADL, w tym rozdzielenie odpowiedzialności na dedykowane jednostki przetwarzające.

# Funkcjonalności systemu:

- Wybór napoju przez użytkownika.
- Symulacja procesu płatności.
- Sterowanie dozowaniem składników i wydawaniem kubka.
- Kontrola procesu podgrzewania wody.
- Wyświetlanie podstawowych statusów i komunikatów dla użytkownika.
- Monitorowanie kluczowych parametrów (np. temperatura wody, uproszczony stan zapasów).
- Obsługa przycisku awaryjnego zatrzymania.
- Dedykowane monitorowanie krytycznych parametrów bezpieczeństwa (np. przegrzanie).
- Możliwość wysyłania zagregowanych informacji o stanie automatu oraz raportów o stanie zdrowia systemu przez sieć (uproszczona symulacja).

# Komponenty modelu:

### Pakiet
- `vending_machine` – główny pakiet grupujący wszystkie elementy modelu automatu.

### System
- `VendingMachine_Sys` – główny komponent systemowy, integrujący podsystemy automatu.

### Procesory
- `Control_Cpu` – procesor wykonujący główną logikę sterowania automatem oraz obsługę wejścia/wyjścia.
- `Safety_Cpu` – dedykowany procesor dla krytycznych funkcji bezpieczeństwa.

### Pamięci
- `Control_Mem` – pamięć operacyjna dla `Control_Cpu` i danych systemu.
- `Safety_Mem` – pamięć operacyjna dla `Safety_Cpu` i danych systemu bezpieczeństwa.

### Magistrale
- `System_Bus` – główna magistrala systemowa do komunikacji między kluczowymi komponentami.
- `Network_Bus` – magistrala do komunikacji z modułem sieciowym.

### Typy Danych (przykładowe, w kodzie bardziej szczegółowe)
- `BeverageOrderData`, `PaymentInfoData`, `WaterConditionData`, `InventoryStatusData`, `MachineDisplayData`, `ExternalCommandData`.
- `OutgoingNetworkData` – zagregowane dane wysyłane przez sieć.
- `Safety_Status_Data` – dane o stanie systemu bezpieczeństwa.

### Procesy
- `InputSensingProcess` (na `Control_Cpu`) – proces zbierający dane z sensorów i wejść użytkownika.
- `MainControlExecutionProcess` (na `Control_Cpu`) – proces wykonujący główną logikę sterowania i komunikację.
- `Safety_Supervision_Process` (na `Safety_Cpu`) – proces odpowiedzialny za monitorowanie bezpieczeństwa i reakcję na zagrożenia.

### Wątki (wybrane kluczowe)
- W `InputSensingProcess`:
    - `UserInputMonitorThread`, `PaymentStatusMonitorThread`, `WaterTemperatureMonitorThread`, `InventoryLevelMonitorThread`.
- W `MainControlExecutionProcess`:
    - `VendingControlLogicThread` – główny wątek koordynujący, zarządzający stanem automatu.
    - `NetworkCommandReceiverThread` – wątek odbierający komendy z sieci.
    - `System_Health_Monitor_Thread` – wątek zbierający informacje o stanie systemu, statusie operacyjnym i generujący zagregowane raporty do wysłania przez sieć.
- W `Safety_Supervision_Process`:
    - `Critical_Temperature_Monitor_Thread` – monitoruje temperaturę pod kątem niebezpiecznych wartości.
    - `Emergency_Stop_Handler_Thread` – obsługuje sygnał z przycisku awaryjnego.
    - `Safety_Coordinator_Thread` – koordynuje działania systemu bezpieczeństwa.

### Urządzenia
- `UserSelectionPanel` – panel użytkownika (przyciski, wyświetlacz).
- `PaymentTerminalDevice` – terminal płatniczy.
- `WaterTemperatureSensorDevice` – czujnik temperatury wody.
- `HeaterActuatorDevice` – grzałka (z możliwością awaryjnego wyłączenia).
- `DispensingMechanismDevice` – mechanizm dozujący (z możliwością awaryjnego wyłączenia).
- `InventorySensorDevice` – czujnik zapasów.
- `MachineDisplay` – wyświetlacz statusu.
- `NetworkInterfaceModule` – moduł interfejsu sieciowego.
- `EmergencyStopButtonDevice` – przycisk awaryjnego zatrzymania.

# Diagram Systemu

Poniżej przedstawiono diagram komponentów systemu automatu do gorących napojów.

![Diagram automatu do napojów](vending_machine_diagram.jpg)


# Bibliografia:

1.  SAE International. *AS5506D: Architecture Analysis & Design Language (AADL)*. Kwiecień 2022. `https://www.sae.org/standards/content/as5506/`
2.  Feiler, P. H., Gluch, D. P., & Hudak, J. J. *Model-Based Engineering with AADL: An Introduction to the SAE Architecture Analysis & Design Language*. Addison-Wesley Professional, Wrzesień 2012. `https://www.amazon.com/Model-Based-Engineering-AADL-Introduction-Architecture/dp/0134208897`
3.  Software Engineering Institute, Carnegie Mellon University. *Architecture Analysis and Design Language (AADL)*. `https://insights.sei.cmu.edu/projects/architecture-analysis-and-design-language-aadl/`
4.  *EP1321908A2: Vending machine control system*. Zgłoszony 18 grudnia 2002. `https://patents.google.com/patent/EP1321908A2/en`
