---
layout: post
title: "Konfiguracja Visual Studio Code dla Pythona"
categories: journal
tags: [python]
image: 2025-09-11-python-konfiguracja/laptop-code.jpg
---

Programuję od dawna i w poprzednich miejscach pracy zawsze mieliśmy mniej lub bardziej kompletną instrukcję, jak postawić środowisko. Niedawno zmieniłam pracę i przy konfiguracji wszystkiego od nowa brakowało mi takiej notatki. Postanowiłam stworzyć ją tutaj, jako przypomnienie dla siebie.

Teraz jestem jedyną osobą w firmie programującą w Pythonie, więc jestem zdana sama na siebie. Ta ściąga ma mi ułatwić życie, kiedy kolejny raz będę stawiać środowisko od zera.

Ta instrukcja dotyczy **Visual Studio Code** i **Pythona**. Planuję spisać tu rozszerzenia, ustawienia i inne drobiazgi, które sprawiają, że praca idzie szybciej i wygodniej. To wersja robocza, którą z czasem będę rozwijać o kolejne elementy.

## Rozszerzenia Visual Studio Code dla Pythona

- **Python** – podstawowe rozszerzenie od Microsoftu, które dodaje obsługę Pythona w VS Code: uruchamianie kodu, debugowanie, integracja z interpreterem, wirtualne środowiska.
- **Pylance** – silnik analizy kodu od Microsoftu. Daje szybkie podpowiedzi IntelliSense, sprawdzanie typów, ostrzeżenia, podpowiadanie docstringów. Zdecydowanie poprawia komfort pisania kodu.
- **autopep8** – automatyczne formatowanie kodu zgodnie z PEP 8. (Do zmiany?)
- **Python Indent** – usprawnia zarządzanie wcięciami w Pythonie. VS Code czasem potrafi się pogubić przy blokach kodu – to rozszerzenie pilnuje poprawnych poziomów wcięć.
- **Jupyter** – pozwala otwierać, edytować i uruchamiać notebooki Jupyter (`.ipynb`) bezpośrednio w VS Code. Bardzo wygodne przy prototypowaniu, analizie danych czy testowaniu fragmentów kodu.

## Inne przydatne rozszerzenia Visual Studio

- **Markdown All in One** – rozszerzenie do edycji Markdown. Dodaje skróty klawiszowe, podgląd na żywo, spisy treści, autouzupełnianie nawiasów i linków. Idealne do dokumentacji i notatek.
- **YAML** – obsługa plików .yml i .yaml. Dodaje kolorowanie składni, walidację oraz podpowiedzi (np. do Kubernetes, GitHub Actions, Docker Compose).
- **Makefile Tools** – ułatwia pracę z Makefile. Wykrywa cele (targets), umożliwia ich uruchamianie z poziomu VS Code, integruje się z terminalem.


## Mój plik settings.json

Połączony plik `settings.json` z dwóch komputerów:

```jsonc
{
    // osobiste preferencje
    "editor.wordWrap": "on" 
    "python.analysis.diagnosticMode": "workspace",
    "python.terminal.activateEnvInCurrentTerminal": true,
    "python.analysis.autoFormatStrings": true,
    "python.analysis.typeCheckingMode": "standard",
    "python.analysis.inlayHints.functionReturnTypes": true,
    "python.analysis.inlayHints.variableTypes": true,
    "python.analysis.inlayHints.callArgumentNames": "all",
    "workbench.editor.enablePreview": false,
    "workbench.editor.enablePreviewFromCodeNavigation": false,
    "workbench.editor.closeOnFileDelete": true,

    // pozostałe ustawienia
    "python.languageServer": "Pylance",
    "python.analysis.autoImportCompletions": true,
    "python.analysis.inlayHints.pytestParameters": true,
    "[python]": {
        "editor.defaultFormatter": "ms-python.autopep8"
    }
}
```

Osobiste preferencje:

- `"editor.wordWrap": "on"` – zawijanie linii w edytorze. Bo tak lubię. 
- `"python.analysis.diagnosticMode": "workspace"` – diagnostyka działa na całym workspace (a nie tylko na otwartym pliku!). Kluczowe. W użyciu z linterami zapewnie sprawdzanie całego projektu w trakcie edycji. 
- `"python.terminal.activateEnvInCurrentTerminal: true"` – przy otwieraniu terminala w VS Code automatycznie aktywuje się środowisko wirtualne. (Potencjalnie do wyrzucenia, jeśli przesiądę się na `poetry`?)
- `"python.analysis.autoFormatStrings": true`  – dodaje `f` przed stringiem, gdy dodam w środku zmienną.
- `"python.analysis.typeCheckingMode": "standard"` – sprawdzanie typów na średnim poziomie restrykcyjności.
- `"python.analysis.inlayHints.functionReturnTypes": true`  – podpowiedzi typów zwracanych przez funkcje.
- `"python.analysis.inlayHints.callArgumentNames": "all"` – przy wywołaniach funkcji pokazuje nazwy argumentów.
- `"workbench.editor.enablePreview": false` – każdy plik otwiera się w nowej karcie, zamiast w trybie podglądu, nadpisując bieżącą kartę.
- `"workbench.editor.enablePreviewFromCodeNavigation": false` – pliki otwarte np. przez "Go to Definition" trafiają do normalnej karty, a nie do trybu podglądu.
- `"workbench.editor.closeOnFileDelete": true` – karta automatycznie zamyka się, gdy plik zostanie usunięty z dysku.

Inne ustawienia:
- `"python.languageServer": "Pylance"` – Pylance jako language server. Standard. (Choć w nowszych wersjach VS Code nie ma tego w `settings.json`.)
- `"python.analysis.autoImportCompletions": true` – automatyczne podpowiedzi importów, gdy korzystam z modułów jeszcze niezaimportowanych.
- `"python.analysis.inlayHints.pytestParameters": true` – specjalne inlay hints dla parametrów w testach **pytest**.
- `"editor.defaultFormatter": "ms-python.autopep8"` – domyślny formatter dla Pythona ustawiony na **autopep8**. Pewnie do zmiany, bo Internet poleca inne formattery.

<!--

```json
{
    "python.languageServer": "Pylance",
    "python.analysis.languageServerMode": "full",
    "python.analysis.typeCheckingMode": "standard",
    "python.analysis.diagnosticMode": "workspace",
    "python.terminal.activateEnvInCurrentTerminal": true,

    "python.analysis.autoImportCompletions": true,
    "python.analysis.autoFormatStrings": true,

    "python.analysis.inlayHints.functionReturnTypes": true,
    "python.analysis.inlayHints.variableTypes": true,
    "python.analysis.inlayHints.callArgumentNames": "all",
    "python.analysis.inlayHints.pytestParameters": true,

    "[python]": {
        "editor.defaultFormatter": "ms-python.autopep8"
    }
}
```



* **`python.analysis.languageServerMode: "full"`**
  → Pylance działa w trybie pełnym (pełna analiza całego workspace).


* **`[python].editor.defaultFormatter: "ms-python.autopep8"`**
  → **autopep8** jako domyślny formatter dla plików `.py`.

-->



