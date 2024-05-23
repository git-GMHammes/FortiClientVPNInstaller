# FortiClientVPNInstaller

> Instalador automatizado e gerenciador do FortiClient VPN para conexões corporativas seguras

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux%20%7C%20macOS-lightgrey)](https://github.com)
[![Version](https://img.shields.io/badge/version-1.0.0-blue)](https://github.com)

## 📋 Índice

- [Sobre o Projeto](#sobre-o-projeto)
- [Funcionalidades](#funcionalidades)
- [Pré-requisitos](#pré-requisitos)
- [Instalação](#instalação)
  - [Windows](#windows)
  - [Linux](#linux)
  - [macOS](#macos)
- [Configuração](#configuração)
  - [Configuração Básica](#configuração-básica)
  - [Configuração Avançada](#configuração-avançada)
- [Utilização](#utilização)
  - [Primeiro Uso](#primeiro-uso)
  - [Conectar à VPN](#conectar-à-vpn)
  - [Desconectar](#desconectar)
- [Solução de Problemas](#solução-de-problemas)
- [FAQ](#faq)
- [Contribuindo](#contribuindo)
- [Licença](#licença)
- [Contato](#contato)

## 🎯 Sobre o Projeto

O **FortiClientVPNInstaller** é uma solução automatizada para instalação, configuração e gerenciamento do FortiClient VPN. Este projeto simplifica o processo de deployment do cliente VPN em ambientes corporativos, permitindo configurações padronizadas e facilitando a manutenção.

### Por que usar este instalador?

- ✅ Instalação automatizada e sem interação do usuário
- ✅ Configurações pré-definidas para ambientes corporativos
- ✅ Suporte multiplataforma (Windows, Linux, macOS)
- ✅ Scripts de atualização e manutenção inclusos
- ✅ Rollback automático em caso de falhas
- ✅ Logs detalhados para troubleshooting

## ⚡ Funcionalidades

- **Instalação Silenciosa**: Deploy sem interação do usuário
- **Configuração Automática**: Import de perfis VPN pré-configurados
- **Multi-perfil**: Suporte para múltiplos perfis de conexão
- **Auto-update**: Verificação e atualização automática do cliente
- **Backup de Configurações**: Backup automático antes de atualizações
- **Integração com AD/LDAP**: Suporte para autenticação corporativa
- **Monitoramento**: Scripts para verificação de status da conexão

## 📦 Pré-requisitos

### Requisitos de Sistema

#### Windows

- Windows 10/11 (64-bit) ou Windows Server 2016+
- .NET Framework 4.7.2 ou superior
- Privilégios de administrador
- 200 MB de espaço em disco

#### Linux

- Ubuntu 20.04+, Debian 10+, CentOS 8+, ou Red Hat 8+
- Kernel 4.x ou superior
- Privilégios de root/sudo
- 150 MB de espaço em disco

#### macOS

- macOS 10.15 (Catalina) ou superior
- Privilégios de administrador
- 200 MB de espaço em disco

### Requisitos de Rede

- Acesso à internet para download dos pacotes
- Portas necessárias:
  - TCP: 443 (HTTPS)
  - UDP: 500, 4500 (IPsec)
  - TCP: 10443 (SSL-VPN)

## 🚀 Instalação

### Windows

#### Método 1: Instalador Executável (Recomendado)

```powershell
# Baixar o instalador
Invoke-WebRequest -Uri "https://github.com/seu-usuario/FortiClientVPNInstaller/releases/latest/download/FortiClientVPN-Setup.exe" -OutFile "FortiClientVPN-Setup.exe"

# Executar instalação silenciosa
.\FortiClientVPN-Setup.exe /S /v"/qn"
```

#### Método 2: Script PowerShell

```powershell
# Clone o repositório
git clone https://github.com/seu-usuario/FortiClientVPNInstaller.git
cd FortiClientVPNInstaller

# Execute o script de instalação
.\scripts\install-windows.ps1
```

#### Método 3: Instalação Manual

1. Baixe o instalador do FortiClient VPN
2. Execute o instalador com privilégios de administrador
3. Siga o assistente de instalação
4. Importe as configurações do repositório

### Linux

#### Ubuntu/Debian

```bash
# Clone o repositório
git clone https://github.com/seu-usuario/FortiClientVPNInstaller.git
cd FortiClientVPNInstaller

# Torne o script executável
chmod +x scripts/install-linux.sh

# Execute o instalador
sudo ./scripts/install-linux.sh
```

#### CentOS/RHEL

```bash
# Clone o repositório
git clone https://github.com/seu-usuario/FortiClientVPNInstaller.git
cd FortiClientVPNInstaller

# Execute o instalador para RHEL
sudo ./scripts/install-rhel.sh
```

### macOS

```bash
# Clone o repositório
git clone https://github.com/seu-usuario/FortiClientVPNInstaller.git
cd FortiClientVPNInstaller

# Torne o script executável
chmod +x scripts/install-macos.sh

# Execute o instalador
sudo ./scripts/install-macos.sh
```

## ⚙️ Configuração

### Configuração Básica

#### 1. Configurar Perfil de Conexão

Edite o arquivo `config/vpn-profile.xml`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<forticlient_configuration>
  <vpn>
    <ssl-vpn>
      <connection name="Empresa VPN">
        <server>vpn.empresa.com.br</server>
        <port>10443</port>
        <authentication>
          <mode>password</mode>
          <certificate_validation>enabled</certificate_validation>
        </authentication>
      </connection>
    </ssl-vpn>
  </vpn>
</forticlient_configuration>
```

#### 2. Importar Configuração

**Windows:**

```powershell
.\scripts\import-config.ps1 -ConfigFile "config\vpn-profile.xml"
```

**Linux/macOS:**

```bash
./scripts/import-config.sh config/vpn-profile.xml
```

### Configuração Avançada

#### Configurar Auto-Connect

Edite `config/settings.json`:

```json
{
  "autoConnect": true,
  "connectionProfile": "Empresa VPN",
  "startOnBoot": true,
  "minimizeToTray": true,
  "notifications": {
    "enabled": true,
    "showConnectionStatus": true
  },
  "security": {
    "savePassword": false,
    "requireCertificate": true,
    "tlsVersion": "1.2"
  }
}
```

#### Configurar Múltiplos Perfis

```bash
# Adicionar novo perfil
./scripts/add-profile.sh --name "Empresa-Filial" --server "vpn-filial.empresa.com.br" --port 10443

# Listar perfis
./scripts/list-profiles.sh

# Definir perfil padrão
./scripts/set-default-profile.sh "Empresa-Filial"
```

## 📖 Utilização

### Primeiro Uso

#### Verificar Instalação

```bash
# Windows
forticlient --version

# Linux/macOS
forticlient-cli --version
```

#### Testar Conectividade

```bash
./scripts/test-connection.sh
```

### Conectar à VPN

#### Interface Gráfica

1. Abra o FortiClient VPN
2. Selecione o perfil "Empresa VPN"
3. Insira suas credenciais
4. Clique em "Conectar"

#### Linha de Comando

**Windows:**

```powershell
# Conectar
forticlient vpn connect -n "Empresa VPN"

# Verificar status
forticlient vpn status
```

**Linux:**

```bash
# Conectar
forticlient-cli vpn connect -n "Empresa VPN"

# Com credenciais inline (não recomendado em produção)
forticlient-cli vpn connect -n "Empresa VPN" -u usuario -p senha
```

**macOS:**

```bash
# Conectar via helper
./scripts/vpn-connect.sh "Empresa VPN"
```

#### Script Automatizado

```bash
# Conectar com credenciais do ambiente
export VPN_USER="seu_usuario"
export VPN_PASS="sua_senha"
./scripts/auto-connect.sh
```

### Desconectar

**Interface Gráfica:**

- Clique com botão direito no ícone da bandeja
- Selecione "Desconectar"

**Linha de Comando:**

```bash
# Windows
forticlient vpn disconnect

# Linux/macOS
forticlient-cli vpn disconnect
```

### Comandos Úteis

```bash
# Verificar status da conexão
./scripts/check-status.sh

# Ver logs de conexão
./scripts/view-logs.sh

# Atualizar cliente
./scripts/update-client.sh

# Backup de configurações
./scripts/backup-config.sh

# Restaurar configurações
./scripts/restore-config.sh backup-20240103.zip
```

## 🔧 Solução de Problemas

### Erro: "Não foi possível conectar ao servidor"

**Causa**: Problema de rede ou firewall bloqueando portas

**Solução**:

```bash
# Verificar conectividade
ping vpn.empresa.com.br

# Testar portas
telnet vpn.empresa.com.br 10443

# Verificar firewall
# Windows
netsh advfirewall show allprofiles

# Linux
sudo iptables -L -n
```

### Erro: "Certificado inválido"

**Causa**: Certificado SSL expirado ou não confiável

**Solução**:

```bash
# Importar certificado raiz
./scripts/import-certificate.sh path/to/root-ca.crt

# Verificar certificados instalados
./scripts/list-certificates.sh
```

### Erro: "Autenticação falhou"

**Causa**: Credenciais incorretas ou expiradas

**Solução**:

1. Verifique suas credenciais
2. Confirme se não há bloqueio de conta
3. Verifique se a senha não expirou
4. Limpe credenciais salvas:

```bash
./scripts/clear-saved-credentials.sh
```

### Conexão lenta ou instável

**Solução**:

```bash
# Verificar latência
./scripts/diagnose-connection.sh

# Mudar protocolo de conexão
./scripts/switch-protocol.sh --protocol UDP

# Otimizar MTU
./scripts/optimize-mtu.sh
```

### Logs de Debug

**Windows:**

```powershell
# Habilitar logs detalhados
.\scripts\enable-debug-logs.ps1

# Visualizar logs
Get-Content "C:\Program Files\Fortinet\FortiClient\logs\vpn.log" -Tail 50 -Wait
```

**Linux/macOS:**

```bash
# Habilitar logs detalhados
./scripts/enable-debug-logs.sh

# Visualizar logs
tail -f /var/log/forticlient/vpn.log
```

## ❓ FAQ

### Como alterar o servidor VPN?

Edite o arquivo `config/vpn-profile.xml` e reimporte a configuração com `./scripts/import-config.sh`.

### Posso ter múltiplos perfis de VPN?

Sim! Use o script `add-profile.sh` para adicionar quantos perfis precisar.

### A senha fica salva?

Por padrão não. Configure `"savePassword": true` em `settings.json` (não recomendado em ambientes corporativos).

### Como atualizar o FortiClient?

Execute `./scripts/update-client.sh` que verificará e instalará atualizações automaticamente.

### Funciona com autenticação de dois fatores?

Sim! O FortiClient suporta 2FA/MFA. Configure em `vpn-profile.xml` com `<two_factor>enabled</two_factor>`.

### Como desinstalar?

```bash
# Windows
.\scripts\uninstall-windows.ps1

# Linux
sudo ./scripts/uninstall-linux.sh

# macOS
sudo ./scripts/uninstall-macos.sh
```

## 🤝 Contribuindo

Contribuições são bem-vindas! Veja como você pode ajudar:

1. Fork o projeto
2. Crie uma branch para sua feature (`git checkout -b feature/NovaFuncionalidade`)
3. Commit suas mudanças (`git commit -m 'Adiciona nova funcionalidade'`)
4. Push para a branch (`git push origin feature/NovaFuncionalidade`)
5. Abra um Pull Request

### Diretrizes de Contribuição

- Siga os padrões de código do projeto
- Adicione testes para novas funcionalidades
- Atualize a documentação conforme necessário
- Mantenha commits atômicos e com mensagens claras

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

## 📧 Contato

- **Repositório**: [https://github.com/seu-usuario/FortiClientVPNInstaller](https://github.com/seu-usuario/FortiClientVPNInstaller)
- **Issues**: [https://github.com/seu-usuario/FortiClientVPNInstaller/issues](https://github.com/seu-usuario/FortiClientVPNInstaller/issues)
- **Wiki**: [https://github.com/seu-usuario/FortiClientVPNInstaller/wiki](https://github.com/seu-usuario/FortiClientVPNInstaller/wiki)

---

## 📚 Recursos Adicionais

- [Documentação Oficial FortiClient](https://docs.fortinet.com/forticlient)
- [Guia de Administrador FortiGate](https://docs.fortinet.com/fortigate)
- [Fórum da Comunidade](https://community.fortinet.com/)
- [Base de Conhecimento](https://kb.fortinet.com/)

## 🔄 Roadmap

- [x] Instalação automatizada
- [x] Suporte Windows, Linux e macOS
- [x] Configuração multi-perfil
- [ ] Interface web para gerenciamento
- [ ] Dashboard de monitoramento
- [ ] Integração com sistemas de ticketing
- [ ] Suporte para deployment via GPO/SCCM
- [ ] App mobile para gerenciamento remoto

## 📊 Status do Projeto

![Status](https://img.shields.io/badge/status-active-success.svg)
![Build](https://img.shields.io/badge/build-passing-brightgreen.svg)
![Coverage](https://img.shields.io/badge/coverage-85%25-green.svg)

---

**Desenvolvido com ❤️ para facilitar a vida dos administradores de rede**
