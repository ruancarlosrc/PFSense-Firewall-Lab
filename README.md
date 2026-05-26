# pfSense Firewall Lab — Simulação de Ataque DoS

---

## Objetivo

Instalar e configurar o pfSense como firewall de rede em ambiente virtualizado e observar o comportamento do tráfego durante um ataque de negação de serviço (DoS) via SYN Flood, capturado em tempo real com Wireshark.

---

## Topologia

```
[Kali Linux] 192.168.1.10  ──→  [pfSense]  ──→  [Alvo] 192.168.1.13
              (atacante)                           (Linux Mint)
```

---

## O que foi feito

**1. Instalação do pfSense CE** — setup via Netgate Installer no VirtualBox, configuração das interfaces WAN e LAN e acesso ao WebConfigurator.

**2. Simulação de SYN Flood (DoS)** — ataque gerado pelo Kali com `hping3` em flood mode direcionado à porta 80 do alvo:

```bash
sudo hping3 -S -p 80 --flood 192.168.1.13
```

Resultado: 2.326.091 pacotes transmitidos, 0 recebidos — alvo sem capacidade de resposta durante o flood.

**3. Captura com Wireshark** — tráfego capturado na interface do alvo (Linux Mint), evidenciando o padrão característico de SYN Flood: rajadas de pacotes TCP SYN do atacante seguidas de RST/ACK do alvo tentando responder.

---

## Evidências

| Arquivo | Conteúdo |
|---|---|
| `Instalando_pfsense.jfif` | Tela de instalação do pfSense CE |
| `Tela_de_acesso_ao_pf.jfif` | Login screen do WebConfigurator |
| `Painel_de_controle.jfif` | Dashboard pfSense 2.8.1 |
| `Comandos_de_ataque_no_kali.jfif` | hping3 flood em execução no Kali |
| `Ataque_DOS.jfif` | Captura Wireshark do SYN Flood (~91k pacotes) |

---
Fonte: Lab original de The Social Dork
