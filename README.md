# door-handler-PragmaDev-Studio

<details><summary>[ENG]</summary>
<p>
Repository of the PragmaDev Studio project consisting of a code-unlocked door system model, expected properties in PSC and two traces of the system's operation.

The design reflects a simple system that unlocks 3 code-protected doors. It consists of 4 processes:
1. PFrontend - the process responsible for pre-processing the signal, rejecting signals whose value does not match the possible expected ones and sending error and status messages. In other words, it acts as a system interface.
2. PBackend - a process whose role is to verify the codes entered via the interface to unlock the door. If successful, it sends a signal to unlock the door.
3. PBHelper - a process supporting PBackend in a situation that simulates going into the "out-of-order" state. You could say it's a backend repair process.
4. D3JammedSim - a process that simulates door jams and 3. failure to open them.

The expected scheme of using the system looks something like this:
1. Send the s_Initialize signal
2. Send the s_Num signal with the parameter value corresponding to the door number you want to unlock
3. Send the s_Num signal 3x with the parameter value corresponding to the number of the current code position (Doors 1: 1 2 3; 2: 2 3 4; 3: 5 6 7)
4. If no error accoured, the door opens. It is possible to unlock another door next from point 2.

In order to obtain the richest possible "internal life" of the system, additional functions have been added to the basic processes:
- When an incorrect digit is entered, the s\_Failed signal is sent with the value 1 in case of wrong door number, 2 in case of wrong code. The system then enters a lockout mode that requires an RST signal.
- In case of unlocking door no. 3 there is a 40% chance that they will jam, in which case s_Failed is 3.
- When entering each digit of the code, there is a 10% chance that the system will go "out-of-order" for a period of 5-20 seconds. After the time has elapsed, re-enter the number.

System board view:
![image](https://github.com/mfedorcz/door-handler-PragmaDev-Studio/assets/105107045/436e7cc8-1c39-4ca1-bacc-553858a746d4)


The requirements in the spec_k_req file are for demonstration purposes only and are not intended to be met for all system traces. These requirements are defined as follows:
1. When the s_Num signal is 6, the s_Wait response is expected
2. When the s_Initialize signal appears, appearance of the s_GO signal after it is considered as failure (signal sent in a different context)
3. The time between sending the s_sysOffline and s_sysOnline signal should not exceed 21 seconds.

View of the spec_k_req board:

![image](https://github.com/mfedorcz/door-handler-PragmaDev-Studio/assets/105107045/eeae25c1-cccd-431c-83f1-6a9c8f38b6f6)
</p>
</details>

Repozytorium projektu PragmaDev Studio składającego sie z modelu systemu drzwi odblokowwywanych kodem i oczekiwanych właściwości zapisancyh w PSC, oraz dwóch śladów działania systemu.

W projekcie został odwierciedlony prosty system odblokowujący 3 drzwi chronione kodem. Składa się on z 4 procesów:
1. PFrontend - proces odpowiedzialny za wstępne przetwarzanie sygnału, odrzucanie sygnałów, których wartość nie odpowiada możliwym oczekiwanym i wysyła komunikaty o błędach i stanie. Innymi słowy pełni rolę interfejsu systemu.
2. PBackend - proces, którego rola to weryfikacja kodów wpisywanych przez interfejs w celu odblokowania drzwi. W przypadku sukcesu wysyła sygnał odblokowujący drzwi.
3. PBHelper - proces wspierający PBackend w sytuacji, która symuluje przejście w stan "out-of-order". Można powiedzieć, że to proces naprawiający backend.
4. D3JammedSim - proces symulujący zacięcia drzwi 3. i niepowodzenie ich otwarcia.

Oczekiwany schemat korzystania z sytemu przedstawia się mniej więcej tak:
1. Wyślij sygnał s_Initialize
2. Wyślij sygnał s_Num z wartością parametru odpowiadającą numerowi drzwi, które chcesz odblokować
3. 3x Wyślij sygnał s_Num z wartością parametru odpowiadającą liczbie aktualnej pozycji kodu (Drzwi 1: 1 2 3; 2: 2 3 4; 3: 5 6 7)
4. Drzwi powinny zostać otwarte, jeśli nie doszło do żadnego błędu, możliwe jest odblokowanie kolejnych drzwi od punktu 2.

W celu uzyskania możliwie bogatego “życia wewnętrznego" systemu do podstawowych procesów zostały dodane dodatkowe funkcje:
- Przy wprowadzeniu błędnej cyfry wysyłany jest sygnał s_Failed z wartośćią 1 w przypadku złego numeru drzwi, 2 w przypadku błędnego kodu. System następnie przechodzi do trybu blokady wymagającego sygnału RST.
-  W przypadku oblokowania drzwi nr. 3 jest 40\% szans, że się zatną, w takim przypadku s_Failed ma wartość 3.
-  Przy wprowadzaniu każdej cyfry kodu jest 10\% szans, że sytem przejdzie do stany "out-of-order" na czas z przedziału 5-20 sekund. Po jego upłynięciu należy wprowadzić ponownie cyfrę.

Widok planszy systemu:
![obraz](https://github.com/mfedorcz/door-handler-PragmaDev-Studio/assets/105107045/436e7cc8-1c39-4ca1-bacc-553858a746d4)


Wymogi w pliku spec_k_req mają charakter jedynie demonstracyjny i nie zakładano, że zostaną spełnione w przypadku wszystkich śladów działania systemu. Te wymagania określono następująco:
1. Przy pojawieniu się sygnału s_Num o wartości 6, oczekuje się odpowiedzi s_Wait
2. Przy pojawieniu się sygnału s_Initialize błedem będzie pojawienie się po nim sygnału s_GO (sygnał nadawany w innym kontekście)
3. Czas pomiędzy nadanie sygnału s_sysOffline, a s_sysOnline nie powinien przekraczać 21 sekund.

Widok planszy spec_k_req:

![obraz](https://github.com/mfedorcz/door-handler-PragmaDev-Studio/assets/105107045/eeae25c1-cccd-431c-83f1-6a9c8f38b6f6)

