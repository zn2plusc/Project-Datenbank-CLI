#### Dokumentation zur Einbindung von Anti-Reverse-Engineering Methoden

## Hier der Download zum Demo Projekt: [Download](https://github.com/josefschmidt0/Project-Datenbank-CLI/raw/main/Datenbank.exe)

Diese Anleitung zeigt, wie Sie die `filepump`-Methoden aus der `file_pump.h` Datei in ein Projekt einbinden und mit **ADVobfuscator** obfuskieren können. Außerdem wird die Installation von GCC mit MSYS2 und MinGW für die Nutzung von `g++` auf Windows beschrieben.

#### Voraussetzungen

1. Ein kompatibler `C++11` oder `C++14` Compiler.
2. Für einige Funktionen wird die [Boost-Bibliothek](https://www.boost.org) benötigt.

#### Installation der Boost-Bibliothek

- Debian/Ubuntu: `sudo apt-get install libboost-all-dev`
- macOS: `brew install boost`
- Windows: [Boost herunterladen](https://www.boost.org/users/download/) und installieren. Pfad in Visual Studio anpassen: `Properties | C/C++ | General | Additional Include Directories`.

#### Installation von GCC mit MSYS2 und MinGW

1. **MSYS2 herunterladen und installieren:**
   - Laden Sie das MSYS2-Installationsprogramm von der [MSYS2-Website](https://www.msys2.org/) herunter.
   - Führen Sie das Installationsprogramm aus und folgen Sie den Anweisungen.

2. **MSYS2 einrichten:**
   - Starten Sie die MSYS2 Shell (MSYS2 MSYS).
   - Aktualisieren Sie das Paket-Datenbank und die installierten Pakete:
     ```sh
     pacman -Syu
     ```

3. **Installation von GCC und G++:**
   - Starten Sie die MSYS2 MinGW 64-bit Shell.
   - Installieren Sie das GCC-Paket:
     ```sh
     pacman -S mingw-w64-x86_64-gcc
     ```

4. **Einrichten der Pfadumgebungsvariable:**
   - Fügen Sie den Pfad zu `mingw64/bin` in Ihre Systemumgebungsvariablen hinzu (meistens unter `C:\msys64\mingw64\bin`).

5. **Überprüfen der Installation:**
   - Öffnen Sie ein neues Kommandozeilenfenster und führen Sie den folgenden Befehl aus, um die Version von `g++` zu überprüfen:
     ```sh
     g++ --version
     ```

#### Schritt-für-Schritt Anleitung

##### 1. ADVobfuscator in das Projekt einbinden

1. Laden Sie **ADVobfuscator** von der [GitHub-Seite](https://github.com/andrivet/ADVobfuscator) herunter.
2. Integrieren Sie die `Lib`-Dateien von **ADVobfuscator** in Ihr Projekt. Kopieren Sie den gesamten Ordner `Lib` in Ihr Projektverzeichnis.

##### 2. Einbindung von file_pump.h

1. Kopieren Sie die `file_pump.h` Datei in Ihr Projektverzeichnis.
2. Integrieren Sie `file_pump.h` in Ihre .cpp Datei, die Sie obfuskieren möchten.

##### 3. Obfuskation der Strings und Funktionsaufrufe

Um die Strings und Funktionsaufrufe in `file_pump.h` zu obfuskieren, verwenden Sie **ADVobfuscator**.

1. **Beispiel-Code mit obfuskierten Strings:**
   ```cpp
   #include "Lib/MetaString.h"
   #include "file_pump.h"
   #include <iostream>

   int main() {
       constexpr auto path = OBFUSCATED("example.txt");
       constexpr auto type = OBFUSCATED("MBs (Megabytes)");
       char output[512];

       long long estimation = generateEstimation(output, path.decrypt(), type.decrypt(), 10);
       std::cout << output << std::endl;

       return 0;
   }
   ```

2. Kompilieren Sie den Code mit Ihrem C++-Compiler:
   ```sh
   g++ -std=c++14 -o obfuscated_example obfuscated_example.cpp
   ```

##### 4. Obfuskation der Funktionsaufrufe

1. **Beispiel-Code mit obfuskierten Funktionsaufrufen:**
   ```cpp
   #include "Lib/ObfuscatedCall.h"
   #include "file_pump.h"
   #include <iostream>

   int main() {
       constexpr auto path = OBFUSCATED("example.txt");
       constexpr auto type = OBFUSCATED("MBs (Megabytes)");
       char output[512];

       OBFUSCATED_CALL(generateEstimation, output, path.decrypt(), type.decrypt(), 10);
       std::cout << output << std::endl;

       return 0;
   }
   ```

2. Kompilieren Sie den Code wie gewohnt:
   ```sh
   g++ -std=c++14 -o obfuscated_call_example obfuscated_call_example.cpp
   ```

##### 5. Weitere Beispiele und Dokumentation

Im `Examples`-Ordner von **ADVobfuscator** finden Sie weitere Beispiele zur Nutzung der Bibliothek. Jedes Beispiel befindet sich in einem eigenen Unterverzeichnis und kann durch Ausführen des Makefiles (`make`) kompiliert werden.

#### Debug Builds

**ADVobfuscator** ist nicht kompatibel mit Debug Builds, da die meisten Optimierungen und spezifische Compileranweisungen in Debug Builds nicht berücksichtigt werden. Verwenden Sie daher immer Release Builds.

#### Unterstützung und Kompatibilität

**ADVobfuscator** wurde mit folgenden Umgebungen getestet:
- Xcode (LLVM) 8.1.0 unter macOS 10.12
- GCC 7.2.0 unter Debian 10
- Visual Studio 2017 (15.3.3) unter Windows 10
- Boost 1.65.0

Andere `C++11/14` kompatible Compiler sollten ebenfalls funktionieren.

### Weiterführende Informationen

Für mehr Details und spezielle Anwendungsfälle besuchen Sie die [GitHub-Seite von ADVobfuscator](https://github.com/andrivet/ADVobfuscator) oder lesen Sie die bereitgestellten Whitepapers und Dokumentationen im `Docs`-Ordner des Projekts.

Andere `C++11/14` kompatible Compiler sollten ebenfalls funktionieren.

### Weiterführende Informationen

Für mehr Details und spezielle Anwendungsfälle besuchen Sie die [GitHub-Seite von ADVobfuscator](https://github.com/andrivet/ADVobfuscator) oder lesen Sie die bereitgestellten Whitepapers und Dokumentationen im `Docs`-Ordner des Projekts.
