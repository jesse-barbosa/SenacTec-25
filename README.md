## 📱 Guia de Instalação e Configuração do Cordova no Windows 10

## OBS: Para facilitar a configuração, instale o Android SDK em *C:\Android\Sdk* e o Gradle em *C:\Gradle* (conforme indicado no passo a passo).

## ✅ Requisitos
- Node.js (LTS) — recomendado: **20.x** (ou >= 20.5)
- npm (vem junto com o Node.js)
- Java JDK 17 (ex.: Eclipse Temurin / Adoptium)
- Android Studio (instalar pelo site oficial)
- Gradle (instale em `C:\Gradle`; versão recomendada: **8.13** ou a versão que seu projeto exigir)
- Dispositivo Android físico com **Modo de Desenvolvedor** e **Depuração USB** ativados

---

## ⚙️ Passo a Passo

### 1) Instalar Node.js e Cordova
1. Baixe e instale o Node.js LTS: https://nodejs.org/pt  
2. Abra um terminal (cmd / PowerShell) e instale o Cordova globalmente:
    npm install -g cordova

### 2) Instalar Android Studio e configurar o local do SDK (C:\Android\Sdk)
1. Baixe e instale o Android Studio: https://developer.android.com/studio?hl=pt-br  
2. Antes de instalar os SDKs, configure o local do SDK para `C:\Android\Sdk`:
   - Abra o Android Studio
   - Na tela inicial clique em **More Actions → SDK Manager**
   - Em **SDK Location** altere **Android SDK Location** para:
       C:\Android\Sdk
   - Salve/Apply

### 3) No SDK Manager: instalar os pacotes necessários
#### Aba **SDK Platforms**
- Marque **Android 14 (API 34)** ou **Android 15 (API 35)** (pelo menos uma)
- Ative **Show Package Details** se quiser escolher itens específicos
- Selecione dentro da plataforma:
  - Android SDK Platform
  - (Opcional) Google APIs
  - (Opcional) Sources for Android

#### Aba **SDK Tools**
- Marque e instale:
  - Android SDK Build-Tools (última versão disponível)
  - Android SDK Platform-Tools
  - Android SDK Command-line Tools (latest)
  - Google USB Driver (Windows)
- Clique em **Apply** e aguarde o download/instalação (será salvo em C:\Android\Sdk)

### 4) Instalar o Gradle em C:\Gradle
1. Baixe a versão desejada do Gradle (ex.: 8.13) em https://gradle.org/releases  
2. Extraia o ZIP em:
    C:\Gradle\gradle-8.13
3. Adicione ao PATH a pasta bin:
    C:\Gradle\gradle-8.13\bin

### 5) Configurar variáveis de ambiente (Windows)
Abra **Painel de Controle → Sistema → Configurações Avançadas → Variáveis de Ambiente** e ajuste:

Variáveis do sistema:
- JAVA_HOME = C:\Program Files\Eclipse Adoptium\jdk-17.0.16.8-hotspot
- ANDROID_HOME = C:\Android\Sdk
- ANDROID_SDK_ROOT = C:\Android\Sdk

Adicionar ao Path (se já não existir, acrescente estas entradas):
- %JAVA_HOME%\bin
- %ANDROID_HOME%\platform-tools
- %ANDROID_HOME%\cmdline-tools\latest\bin
- %ANDROID_HOME%\tools\bin
- C:\Gradle\gradle-8.13\bin

> Após alterar variáveis, **feche e reabra** o terminal para carregar as mudanças.

### 6) Criar projeto Cordova
No terminal:
    cordova create myapp com.example.app MyApp
    cd myapp

### 7) Adicionar plataforma Android
No diretório do projeto:
    cordova platform add android

### 8) Testes básicos (verificar instalações)
No terminal:
    java -version
    node -v
    npm -v
    adb --version
    gradle -v
    cordova requirements

### 9) Preparar o dispositivo e rodar
1. No Android: Ative **Modo de Desenvolvedor** e **Depuração USB**.
2. Conecte o aparelho por cabo USB (use cabo que suporte dados).
3. Confirme a solicitação de depuração no celular (aceite a chave RSA).
4. No terminal, verifique:
    adb devices
   - Deve aparecer algo do tipo: `0123456789abcdef    device`
5. Para compilar e instalar no aparelho:
    cordova run android --device

---

## 🔧 Resolução rápida de problemas comuns

- **`cordova` não encontrado**  
  - Reabra o terminal após `npm install -g cordova`. Certifique-se que o diretório global do npm está no PATH.

- **Erro: JAVA_HOME inválido**  
  - Confirme `echo %JAVA_HOME%` e `java -version`. Ajuste a variável para o caminho real da JDK.

- **Gradle wrapper falha ao baixar `gradle-8.13-bin.zip`**  
  - Baixe manualmente `https://services.gradle.org/distributions/gradle-8.13-bin.zip` e coloque em:
      platforms\android\gradle\wrapper\dists\<alguma-pasta>\
  - Ou edite `platforms/android/gradle/wrapper/gradle-wrapper.properties` e ajuste `distributionUrl` para apontar para a versão que você instalou localmente.

- **`adb devices` não mostra aparelho**  
  - Instale drivers USB do fabricante (ou Google USB Driver via SDK Manager). Use cabo original.

- **XIAOMI: aparelho exige configuração adicional de “Install via USB”**  
1. Vá em **Configurações > Sobre o telefone**, toque várias vezes em **Versão da MIUI** até ativar as **Opções do desenvolvedor**.
2. Dentro de **Configurações > Ajustes adicionais > Opções do desenvolvedor**, desative **MIUI Optimizations** *(se existir)*, ative **USB Debugging** e também **Install via USB**.
3. A ativação de **Install via USB** pode exigir que você faça login com sua **conta Xiaomi (Mi Account)** antes de liberar a instalação via USB.


---

## ✅ Observações finais
- Este guia pressupõe instalação do Android SDK em `C:\Android\Sdk` e do Gradle em `C:\Gradle` (conforme solicitado).  
- Se preferir, pode deixar o SDK na pasta padrão do Android Studio; só ajuste as variáveis `ANDROID_HOME`/`ANDROID_SDK_ROOT` para apontar corretamente.  
- Sempre abra um terminal novo depois de alterar variáveis de ambiente.

---
