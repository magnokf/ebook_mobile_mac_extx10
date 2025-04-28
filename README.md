# ebook_mobile_mac_extx10


# E-book Avançado: Construindo um Ambiente de Desenvolvimento Mobile Profissional no Mac Mini M4 com Disco Externo EXTX10

---

## 📖 Apresentação

Este e-book ensina de forma profunda, técnica e prática como configurar um ambiente de desenvolvimento mobile de alta performance em um Mac Mini M4 utilizando um SSD externo (EXTX10 de 1TB). O conteúdo é ideal para formação de times, treinamentos técnicos e criação de cursos digitais para plataformas como Hotmart.

Ao final, você terá um Mac otimizado para React Native, Expo, Android Studio e Xcode, e poderá ensinar este processo de maneira didática a outros desenvolvedores.

---

# Índice

1. Instalação e Ajustes Iniciais do Android Studio
2. Configuração do Xcode e Simuladores iOS
3. Scripts Profissionais de Otimização
4. Automatizando Manutenção com Automator e Calendário
5. Conceitos Adicionais Importantes
6. Benefícios para Desenvolvedores e Times
7. Conclusão e Próximos Passos

---

# 1. Instalação e Ajustes Iniciais do Android Studio

### 1.1 Instalação do Android Studio
- Baixe pelo site oficial.
- Instale no SSD interno para máximo desempenho.

### 1.2 Correção do Android SDK (Erro Comum)

Erro comum:
```bash
Failed to resolve the Android SDK path
```

**Solução:**
```bash
mkdir -p /Volumes/EXTX10/Android/sdk
```
E adicione ao seu `.zshrc` ou `.bash_profile`:
```bash
export ANDROID_HOME=/Volumes/EXTX10/Android/sdk
export PATH=$ANDROID_HOME/emulator:$ANDROID_HOME/tools:$ANDROID_HOME/tools/bin:$ANDROID_HOME/platform-tools:$PATH
```

### 1.3 Otimização do Gradle

Mover e linkar:
```bash
mv ~/.gradle /Volumes/EXTX10/Gradle
ln -s /Volumes/EXTX10/Gradle ~/.gradle
```

### 1.4 Configuração de Emuladores Android (AVD)

Mover e criar symlink:
```bash
mv ~/.android/avd /Volumes/EXTX10/Android/avd
ln -s /Volumes/EXTX10/Android/avd ~/.android/avd
```

---

# 2. Configuração do Xcode e Simuladores iOS

### 2.1 Solucionando Problemas de Devices

Mover apenas o `data/` de cada simulador:
```bash
mv ~/Library/Developer/CoreSimulator/Devices/<UUID>/data /Volumes/EXTX10/Xcode/SimulatorsData/data-<UUID>
ln -s /Volumes/EXTX10/Xcode/SimulatorsData/data-<UUID> ~/Library/Developer/CoreSimulator/Devices/<UUID>/data
```

### 2.2 Preparação para o Expo/React Native

Após organizar os simuladores:
```bash
npx expo prebuild
npx expo run:ios
```
Certifique-se que o Simulator.app esteja aberto.

---

# 3. Scripts Profissionais de Otimização

### 3.1 Script Automático de Movimentação de Simuladores

`move_simulators.sh`:
```bash
#!/bin/bash
SRC=~/Library/Developer/CoreSimulator/Devices
DST=/Volumes/EXTX10/Xcode/SimulatorsData

for DEVICE in "$SRC"/*; do
  if [ -d "$DEVICE/data" ]; then
    UUID=$(basename "$DEVICE")
    mv "$DEVICE/data" "$DST/data-$UUID"
    ln -s "$DST/data-$UUID" "$DEVICE/data"
  fi
done
```

### 3.2 Script de Limpeza Mensal

`maintenance_monthly.sh`:
```bash
#!/bin/bash
rm -rf ~/Library/Caches/CocoaPods
npm cache clean --force
rm -rf ~/.expo ~/.eas
rm -rf ~/Library/Developer/Xcode/DerivedData
rm -rf ~/Library/Developer/Xcode/Archives
rm -rf node_modules/.cache/metro
```

### 3.3 Script Avançado com Log e Notificação

`maintenance_monthly_notified.sh`:
```bash
#!/bin/bash
LOG=~/Desktop/maintenance_log.txt

log() {
  echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" >> $LOG
}

log "Iniciando manutenção..."
rm -rf ~/Library/Caches/CocoaPods && log "CocoaPods limpo"
npm cache clean --force && log "npm cache limpo"
rm -rf ~/.expo ~/.eas && log "Expo/EAS limpos"
rm -rf ~/Library/Developer/Xcode/DerivedData && log "DerivedData limpo"
rm -rf ~/Library/Developer/Xcode/Archives && log "Archives limpos"
rm -rf node_modules/.cache/metro && log "Metro Bundler limpo"
osascript -e 'display notification "Manutenção mensal concluída!" with title "Maintenance Mode"'
```

---

# 4. Automatizando Manutenção com Automator e Calendário

### 4.1 Criando o Aplicativo no Automator

- Crie novo aplicativo.
- Adicione "Executar Script de Shell".
- Comando:
```bash
/Volumes/EXTX10/Automator/maintenance_monthly_notified.sh
```
- Salve como `MaintenanceMode.app`.

### 4.2 Agendamento via Calendar

- Criar novo evento "Manutenção Mensal".
- Configurar repetição "Todo Mês".
- Alerta: "Abrir Arquivo" selecionando `MaintenanceMode.app`.

### 4.3 Atenção

Certifique-se de que o EXTX10 esteja conectado para que o script funcione.

---

# 5. Conceitos Adicionais Importantes

- **Symlinks**: Evitam duplicação de dados, liberam espaço e mantêm sistemas funcionando.
- **Logs de manutenção**: Úteis para auditoria de sistemas e histórico de boas práticas.
- **Manter o Automator e scripts atualizados**: Sempre revisar após atualizações de sistema.

---

# 6. Benefícios Reais para Desenvolvedores e Times

- SSD interno livre e desempenho máximo.
- Builds mais rápidos e estáveis.
- Redução de bugs relacionados a cache.
- Treinamentos prontos para capacitar novos colaboradores.
- Base técnica sólida para venda de cursos e mentorias.

---

# 7. Conclusão e Próximos Passos

Implementar esse conjunto de práticas transforma o Mac Mini M4 em uma máquina de desenvolvimento de elite.

**Próximos passos sugeridos:**
- Criar ícones e interface para scripts.
- Separar logs de manutenção por mês.
- Configurar CI/CD para automação total de builds.

Este material pode ser usado como curso online, formação interna de equipes ou monetizado como produto digital premium.

**Fim do E-book**
