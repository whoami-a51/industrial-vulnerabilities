# ⚠️ Exposição Crítica de Sistema SCADA de Controle de Turbinas Eólicas

## 📌 Resumo

Um painel SCADA exposto da Itália, responsável pelo controle de turbinas eólicas, foi encontrado com acesso direto a portas e serviços críticos. Isso inclui uma interface web com certificado SSL válido emitido pela Siemens, uma porta VNC aberta exigindo autenticação por senha (credenciais desconhecidas) e uma porta aberta para comunicação com CLPs Siemens S7 (porta 102). Essa exposição representa um risco severo, com possibilidade de controle remoto das turbinas por agentes não autorizados.
  
![descrição](/imgs/target_1/turbinas.png)  
  

---

## 🔍 Detalhes Técnicos

- **IP Alvo**: `xxx.xxx.xxx.214`

- **Portas Abertas**:
  - `443/tcp (HTTPS)`: Painel de controle web do sistema de turbinas eólicas
  - `5900/tcp (VNC)`: Servidor VNC com autenticação por senha (`VncAuth`, senha desconhecida)
  - `8081/tcp (HTTP)`: Serviço web adicional
  - `102/tcp (iso-tsap)`: Porta de comunicação com CLP Siemens S7 (protocolo S7comm)

- **Certificado SSL**:
  - Emitido por: **Siemens TIA Project** – `NegMicon500_11_cert (EC)`
  - Validade: **20/03/2023** a **20/03/2037**
  - CN: `NegMicon52/Webserver-4`
  - Subject Alternative Names (SANs):
    - `192.168.4.10` (IP interno)
    - `xxx.xxx.xxx.214` (IP externo)

- **Informações do CLP**:
  - **Modelo**: `CPU 1510SP-1 PN`
  - **Nome da estação**: `ET 200SP station_1`
  - **Modo de operação**: `RUN`
  - **Status**: `OK`
  
![descrição](/imgs/target_1/plc.png)  
  

---

## 🧪 Evidências

- A porta TCP `102` está aberta e responde à sondagem; tentativas de comunicação via biblioteca `snap7` falharam com `timeout`, sugerindo uso de firewall ou controle parcial.
- A porta `5900` (VNC) aceita conexões, mas reinicia imediatamente após falha de autenticação. A ausência de bloqueio ou CAPTCHA indica configuração insegura.
- A interface web está disponível via `HTTPS` e `HTTP`, com certificado SSL legítimo emitido pela Siemens — confirmando a autenticidade da plataforma.

![descrição](/imgs/target_1/vnc.jpg)  

  
---

## ⚠️ Riscos

A exposição de um sistema SCADA/ICS de controle de turbinas sem mecanismos robustos de autenticação pode permitir:

- Controle remoto não autorizado das turbinas (ex: iniciar/parar, alterar parâmetros)
- Interrupção na geração de energia e possíveis danos físicos ao equipamento
- Riscos operacionais, ambientais e de segurança
- Ataques cibernéticos direcionados com impacto econômico e reputacional, como uso de Stuxnet
  
![descrição](/imgs/target_1/controles.png)  
  
---

## ✅ Recomendações

- Isolar totalmente os sistemas SCADA da internet pública, limitando o acesso apenas via VPNs e redes internas confiáveis.
- Aplicar autenticação forte no VNC, com senhas seguras e exclusivas. Considere usar autenticação multifator (MFA).
- Implementar firewalls e monitoramento contínuo das portas críticas (102, 5900, 443, 8081).
- Manter o Siemens TIA Portal, firmwares e software relacionados sempre atualizados com os últimos patches de segurança.
- Realizar auditorias de segurança completas e testes de intrusão voltados para a infraestrutura ICS/SCADA.

---

> Este relatório foi produzido com o objetivo de promover a conscientização em cibersegurança para ambientes industriais (ICS/SCADA). Nenhuma alteração foi realizada nos sistemas analisados.

**Relatório gerado por:**
`Whoami-a51`  
