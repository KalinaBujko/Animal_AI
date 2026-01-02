# Animal_AI (UE5 Plugin)

Projekt przedstawia **plugin narzędziowy dla Unreal Engine 5**, którego celem jest wsparcie **testowania, obserwacji (debugowania) oraz ręcznego sterowania stanami AI zwierząt w czasie rzeczywistym**.  
Rozwiązanie nie zastępuje logiki zachowania zwierząt – działa jako **warstwa kontrolno-diagnostyczna**, która porządkuje pracę nad AI w scenach z wieloma instancjami.

## Opis projektu

Plugin umożliwia:
- **podgląd aktualnych stanów AI** aktywnych zwierząt w scenie,
- **wymuszanie stanów** dla pojedynczej instancji lub grupy (operacje zbiorcze),
- **szybkie, powtarzalne testy scenariuszowe** bez konieczności “czekania” na bodźce środowiskowe,
- weryfikację **spójności zachowania i animacji** (stan steruje również Animation Blueprintami).

Rozwiązanie zostało zweryfikowane w scenie demonstracyjnej zawierającej kilka instancji zwierząt (m.in. **lwy** i **hipopotamy**) z prostymi zachowaniami oraz dedykowanymi **Animation Blueprintami zależnymi od stanu**.

## Architektura (przepływ)

Główny przepływ integracji wygląda następująco:

**UI (UMG) → Rejestr aktorów → Interfejs → AIStateManager → Animation Blueprint**

- **UI (WBP_AIStateControl)** – panel testowy w UMG do wyboru aktorów i wymuszania stanów.
- **Rejestr/koordynator** – utrzymuje listę aktywnych instancji i pośredniczy w operacjach zbiorczych.
- **Interfejs (BPI_AnimalStateActions)** – ujednolicone połączenie z aktorami (bez zależności od klas gatunków).
- **AIStateManager (BP_AIStateManager)** – lokalny menadżer stanu w aktorze; przechowuje enum i propaguje zmiany.
- **AnimBP (ABP_)** – animacje przełączane na podstawie bieżącego stanu.

## Model stanu

Wspólny model stanu jest zdefiniowany jako **enum** (np. `E_AnimalState`).  
Stany obejmują zarówno rutyny, jak i reakcje sytuacyjne (np. `Idle`, `Roam`, `Eating`, `Alert`, `Flee`, `Aggressive` – zależnie od konfiguracji sceny/projektu).

## Scena demonstracyjna i testy

Plugin był testowany pod kątem:
- automatycznej rejestracji aktorów po uruchomieniu sceny,
- spójności stanu pomiędzy UI a aktorem,
- ręcznego wymuszania stanu dla pojedynczego aktora,
- operacji zbiorczych na wielu instancjach,
- stabilności przejść między stanami oraz synchronizacji z animacją.

## Technologie

- Unreal Engine 5
- Blueprints (UMG, interfejsy, logika runtime)
- Podstawowe systemy AI UE5 (Behavior Trees / Blackboard – zależnie od konfiguracji)
- Animation Blueprints (animacje sterowane stanem)
- Nawigacja (NavMesh) – w scenie demonstracyjnej


