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

# Rozszerzenia Visual Studio Code dla Pythona

- **Python** – podstawowe rozszerzenie od Microsoftu, które dodaje obsługę Pythona w VS Code: uruchamianie kodu, debugowanie, integracja z interpreterem, wirtualne środowiska.
- **Pylance** – silnik analizy kodu od Microsoftu. Daje szybkie podpowiedzi IntelliSense, sprawdzanie typów, ostrzeżenia, podpowiadanie docstringów. Zdecydowanie poprawia komfort pisania kodu.
- **autopep8** – automatyczne formatowanie kodu zgodnie z PEP 8. 
- **Python Indent** – usprawnia zarządzanie wcięciami w Pythonie. VS Code czasem potrafi się pogubić przy blokach kodu – to rozszerzenie pilnuje poprawnych poziomów wcięć.
- **Jupyter** – pozwala otwierać, edytować i uruchamiać notebooki Jupyter (`.ipynb`) bezpośrednio w VS Code. Bardzo wygodne przy prototypowaniu, analizie danych czy testowaniu fragmentów kodu.

# Inne przydatne rozszerzenia Visual Studio

- **Markdown All in One** – rozszerzenie do edycji Markdown. Dodaje skróty klawiszowe, podgląd na żywo, spisy treści, autouzupełnianie nawiasów i linków. Idealne do dokumentacji i notatek.
- **YAML** – obsługa plików .yml i .yaml. Dodaje kolorowanie składni, walidację oraz podpowiedzi (np. do Kubernetes, GitHub Actions, Docker Compose).
- **Makefile Tools** – ułatwia pracę z Makefile. Wykrywa cele (targets), umożliwia ich uruchamianie z poziomu VS Code, integruje się z terminalem.


# Mój plik settings.json

Tak wygląda mój `settings.json` na komputerze nr 1:

```json
{
    "python.languageServer": "Pylance",
    "python.analysis.typeCheckingMode": "standard",
    "python.analysis.diagnosticMode": "workspace",
    "python.analysis.autoImportCompletions": true,
    "python.analysis.autoFormatStrings": true,
    "python.analysis.inlayHints.functionReturnTypes": true,
    "python.analysis.inlayHints.variableTypes": true,
    "python.analysis.inlayHints.callArgumentNames": "all",
    "python.analysis.inlayHints.pytestParameters": true,
    "editor.defaultFormatter": "ms-python.autopep8",
    "editor.wordWrap": "on" 
}
```

Co to znaczy:

- `"python.languageServer": "Pylance"` – Pylance jako language server.
- `"python.analysis.diagnosticMode": "workspace"` – diagnostyka działa na całym workspace (a nie tylko na otwartym pliku!). Prawie jak kompilator.
- `"python.analysis.typeCheckingMode": "standard"` – sprawdzanie typów na średnim poziomie restrykcyjności.
- `"python.analysis.autoImportCompletions": true`  – automatyczne podpowiedzi importów, gdy korzystam z niezaincludowanych jeszcze modułów.
- `"python.analysis.autoFormatStrings": true`  – automatyczne formatowanie f-stringów i stringów.
- `"python.analysis.inlayHints.functionReturnTypes": true`  – podpowiedzi typów zwracanych przez funkcje.
- `"python.analysis.inlayHints.variableTypes": true`  – podpowiedzi typów zmiennych.
- `"python.analysis.inlayHints.callArgumentNames": "all"` – przy wywołaniach funkcji pokazuje nazwy argumentów.
- `"python.analysis.inlayHints.pytestParameters": true` – specjalne inlay hints dla parametrów w testach **pytest**.
- `"editor.defaultFormatter": "ms-python.autopep8"` – domyślny formatter ustawiony na **autopep8**, żeby kod zawsze był zgodny z PEP 8.
- `"editor.wordWrap": "on"` – zawijanie linii w edytorze.

