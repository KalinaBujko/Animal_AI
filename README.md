# Animal_AI UE5 Plugin

Projekt przedstawia **plugin narzędziowy dla Unreal Engine 5**, którego celem jest wsparcie **testowania, obserwacji (debugowania) oraz ręcznego sterowania stanami AI zwierząt w czasie rzeczywistym**.  

## Opis projektu

Plugin umożliwia:
- **podgląd aktualnych stanów AI** aktywnych zwierząt w scenie,
- **wymuszanie stanów** dla pojedynczej instancji lub grupy (operacje zbiorcze),
- **szybkie, powtarzalne testy scenariuszowe** bez konieczności “czekania” na bodźce środowiskowe,
- weryfikację **spójności zachowania i animacji** (stan steruje również Animation Blueprintami).

## Architektura 

**UI (WBP) → Rejestr aktorów → Interfejs → AIStateManager → Animation Blueprint**

- **UI (WBP_AIStateControl)** – panel testowy w UMG do wyboru aktorów i wymuszania stanów.
- **Rejestr/koordynator** – utrzymuje listę aktywnych instancji i pośredniczy w operacjach zbiorczych.
- **Interfejs (BPI_AnimalStateActions)** – ujednolicone połączenie z aktorami (bez zależności od klas gatunków).
- **AIStateManager (BP_AIStateManager)** – lokalny menadżer stanu w aktorze; przechowuje enum i propaguje zmiany.
- **AnimBP (ABP_)** – animacje przełączane na podstawie bieżącego stanu.

## Model stanu

Wspólny model stanu jest zdefiniowany jako **enum** (np. `E_AnimalState`).  
Stany obejmują zarówno rutyny, jak i reakcje sytuacyjne (np. `Idle`, `Roam`, `Eating`, `Alert`, `Flee`, `Aggressive` – zależnie od konfiguracji sceny/projektu).

## Technologie

- Unreal Engine 5
- Blueprints (UMG, interfejsy, logika runtime)
- Podstawowe systemy AI UE5 (Behavior Trees / Blackboard – zależnie od konfiguracji)
- Animation Blueprints (animacje sterowane stanem)
- Nawigacja (NavMesh) – w scenie demonstracyjnej


