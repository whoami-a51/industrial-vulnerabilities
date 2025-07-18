## Exposição de Dois Dispositivos OPND em Rede Industrial

## 🧠 Contexto

Durante a continuidade da pesquisa OSINT voltada para a exposição de infraestruturas SCADA e ICS, foram identificados **dois dispositivos OPND** (Operational Network Peripheral Device) acessíveis via IPs públicos. Ambos estavam localizados na **República Tcheca**, com acesso remoto desprotegido e exibindo em tempo real valores de sensores de temperatura, umidade e outros parâmetros de uma infraestrutura industrial de Data Center.
  
![descrição](/imgs/target_3/data%20center%201.png)    
  
![descrição](/imgs/target_3/data%20center%202.png)    
  
---

## 📂 Dispositivos Identificados

| IP               | Localização          | Status   | Informções Sensíveis            |
|------------------|------------------------|----------|------------------------------|
| xxx.xxx.xxx.169  | Zlin, Czech Republic   | Online   | Interface de controle ativa   |
| xxx.xxx.xxx.170  | Zlin, Czech Republic   | Online   | Interface de controle ativa |

---

## ⚡️ Vetores de Acesso Utilizados

- **Shodan**: descoberta de dispositivos por fingerprint ("OPND Web Server")
- **Porta 80/TCP**: acesso direto ao painel HTTP sem autenticação
- **Inspeção Manual**: identificação de sensores e controles remotos expostos
- **Porta 109/TCP**: tentativas de comunicação via protocolo ISO-on-TCP (utilizado por PLCs Siemens) resultaram consistentemente em Connection timed out, indicando que a porta está filtrada ou dropando conexões silenciosamente. Tentativas em múltiplos racks e slots (0–5) não obtiveram resposta. Há possibilidade de firewall industrial ou ACL de camada 3/4 negando interação externa.
- **Porta 5900/TCP (VNC)**: servidor VNC acessível publicamente; conexão estabelecida, mas encerrada com erro Connection reset by peer, sugerindo bloqueio por política ou exigência de autenticação específica
- **Inspeção Manual**: identificação de sensores, atuadores e controles remotos expostos via interfaces web e serviços auxiliares

---

## ⚠️ Riscos Associados

- **Ataque Físico Remoto**: alteração de parâmetros ambientais
- **Paralisação de Infraestrutura**: risco de superaquecimento de servidores ou linhas de produção
- **Escalonamento de Ataques**: uso da rede local como ponto pivô para ataques laterais
- **Não conformidade com normas industriais** como **IEC 62443**, **NIS2** e **ISO 27001**
  
![descriçãp](/imgs/target_3/controle%20de%20temp%201.png)
![descrição](/imgs/target_3/input%20de%20entrada.png)
![descrição](/imgs/target_3/controle%20de%20temp%202.png)
![descrição](/imgs/target_3/vnc.jpg)
![descrição](/imgs/target_3/iso.jpg)
  
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

**Relatório gerado por:**
`Whoami-a51`  
