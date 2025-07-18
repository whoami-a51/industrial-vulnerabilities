# Relatório de Exposição SCADA — Siemens S7-1200

## 🔍 Resumo

Foi identificado um painel SCADA exposto relacionado a um controlador Siemens S7-1200. Ele estava acessível via HTTP/HTTPS e possuía um certificado SSL válido emitido pela Siemens. Portas industriais críticas estavam abertas — notadamente VNC (5900) e ISO-TSAP (102). Embora a comunicação direta com o PLC tenha expirado (timeout), essa acessibilidade parcial ainda representa um risco significativo de segurança.

## 🌐 Informações do Alvo

- **Endereço IP:** `xx.xxx.xxx.188`  
- **Localização:** Bucareste, Romênia  
- **ISP/Organização:** XXXX ROMANIA S.A / XXXXX Business  
- **Domínio:** `xxxxxxx.ro`

## 🚪 Portas Abertas

| Porta | Protocolo | Serviço          | Observações                          |
|-------|-----------|------------------|------------------------------------|
| 80    | TCP       | HTTP             | Página de login customizada Siemens|
| 443   | TCP       | HTTPS            | Certificado Siemens válido          |
| 102   | TCP       | ISO-TSAP (S7comm)| Comunicação Siemens S7 PLC          |
| 5900  | TCP       | VNC              | VncAuth ativado (senha requerida)   |

## 🔐 Detalhes do Certificado SSL

- **Nome Comum (CN):** `192.168.1.10`  
- **Emissor:** Siemens AG — Família Controladores S7-1200  
- **Validade:** 31 de Dezembro de 2011 até 1º de Janeiro de 2042  
- **Nomes Alternativos (SAN):** Inclui IP interno `192.168.1.10`

## 🧠 Informações do PLC

- **Modelo:** Siemens S7-1200  
- **Status da Comunicação:** Timeout na porta 102 (provavelmente protegido por ACL/firewall)  
- **Método de Acesso Tentado:** ISO-TSAP (porta 102)
  
![descrição](/imgs/target_2/plcs.png)   
  
![descrição](/imgs/target_2/plc1.png)    
  
![descrição](/imgs/target_2/plc2.png)    
  

## 🖥️ Detalhes do VNC

- **Porta:** `5900`  
- **Segurança:** VncAuth (protegido por senha)  
- **Status:** Conexão aceita, falha no login devido a senha desconhecida
  
![descrição](/imgs/target_2/vnc.png)    
  
## 📸 Resumo das Evidências

- Painéis de login web servidos pelas portas `80` e `443`  
- Certificado SSL emitido pela Siemens AG confirmando hardware legítimo  
- Porta VNC aberta, permitindo conexões, mas rejeitando logins não autenticados  
- Porta `102` aberta, indicando exposição da pilha PLC  
- Escaneamentos externos confirmam que a interface SCADA está parcialmente acessível pela internet

## ⚠️ Riscos

- **Exposição da Interface Web:** Pode ser alvo de ataques de força bruta ou exploração remota  
- **Exposição da Porta PLC:** Pode permitir manipulação de baixo nível via pacotes ISO-TSAP personalizados  
- **Exposição do VNC:** Vetor comum de ataque, especialmente se senhas forem fracas ou padrão  
- **Tipo de Sistema:** Industrial — comprometimento pode afetar processos físicos, segurança e operações

## ✅ Recomendações

1. **Remover sistemas SCADA/PLC da internet pública.**  
2. **Utilizar VPNs ou redes internas segmentadas para todo acesso.**  
3. **Aplicar senhas fortes e autenticação multifator sempre que possível (VNC, interface web).**  
4. **Atualizar firmware Siemens para corrigir vulnerabilidades conhecidas.**  
5. **Restringir as portas ISO-TSAP e VNC via regras de firewall.**  
6. **Monitorar todas as tentativas de autenticação e atividade nas portas.**

---

> ⚠️ Este relatório é fornecido para fins educacionais e de divulgação responsável.

**Relatório gerado por:** `Whoami-a51`  
**Data:** `18 de julho de 2025`
