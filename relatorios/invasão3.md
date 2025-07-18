# Relatório de Invasão 3 — Exposição de Dois Dispositivos OPND em Rede Industrial

## 🧠 Contexto

Durante a continuidade da pesquisa OSINT voltada para a exposição de infraestruturas SCADA e ICS, foram identificados **dois dispositivos OPND** (Operational Network Peripheral Device) acessíveis via IPs públicos. Ambos estavam localizados na **República Tcheca**, com acesso remoto desprotegido e exibindo em tempo real valores de sensores de temperatura e umidade de uma infraestrutura industrial.

---

## 📂 Dispositivos Identificados

| IP               | Localização          | Status   | Informções Sensíveis            |
|------------------|------------------------|----------|------------------------------|
| xxx.xxx.xxx.169  | Zlin, Czech Republic   | Online   | Temperatura, Umidade, Logs   |
| xxx.xxx.xxx.170  | Zlin, Czech Republic   | Online   | Interface de controle ativa |

---

## ⚡️ Vetores de Acesso Utilizados

- **Shodan**: descoberta de dispositivos por fingerprint ("OPND Web Server")
- **Porta 80/TCP**: acesso direto ao painel HTTP sem autenticação
- **Inspeção Manual**: identificação de sensores e controles remotos expostos

---

## ⚠️ Riscos Associados

- **Ataque Físico Remoto**: alteração de parâmetros ambientais
- **Paralisação de Infraestrutura**: risco de superaquecimento de servidores ou linhas de produção
- **Escalonamento de Ataques**: uso da rede local como ponto pivô para ataques laterais
- **Não conformidade com normas industriais** como **IEC 62443**, **NIS2** e **ISO 27001**

---

## 🔎 Evidências

- Capturas de tela dos paineis com gráficos de temperatura/umidade em tempo real
- Headers HTTP indicando versão do firmware OPND
- Identificação de redes internas nos scripts de diagnóstico dos painéis

---

## ✅ Recomendações

1. **Isolamento imediato** dos dispositivos de redes públicas
2. Implementar **firewalls industriais** (e.g. FortiGate/SCADA) com ACLs
3. Habilitar autenticação e criptografia (TLS) nos paineis HTTP
4. Auditar possíveis backdoors em dispositivos similares
5. Aplicar segmentação de rede via VLANs e monitoramento passivo (IDS/ICS-SIEM)

---

## 📄 Conclusão

A exposição de dispositivos OPND em redes industriais representa um dos vetores mais críticos de comprometimento de sistemas físicos. O controle ambiental pode parecer inofensivo, mas é um elo frágil que, explorado, pode levar a falhas catastróficas, especialmente em ambientes de produção e data centers.

> Este relatório foi produzido com o objetivo de promover a conscientização em cibersegurança para ambientes industriais (ICS/SCADA). Nenhuma alteração foi realizada nos sistemas analisados.

