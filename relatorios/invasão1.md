# Relatório de Exposição SCADA — Siemens S7-1200

## Resumo

Foi identificado um painel SCADA exposto na internet - atráves do GHDB e Shodan, vinculado a um controlador Siemens S7-1200, acessível via HTTP/HTTPS com certificado SSL legítimo da Siemens. Estão abertas portas críticas como VNC (porta 5900) e a porta 102 (ISO-TSAP) usada para comunicação com PLC. Tentativas de comunicação direta com o PLC resultaram em timeout, indicando possível proteção ou firewall. O VNC exige senha, mas pode ser vulnerável a senhas fracas.

## Detalhes Técnicos

- **IP alvo:** `xxx.xxx.xxx.188`
- **Portas abertas:**
  - 80/tcp (HTTP) – página de login customizada
  - 443/tcp (HTTPS) – página de login com certificado Siemens válido
  - 102/tcp (ISO-TSAP) – porta de comunicação Siemens S7 PLC
  - 5900/tcp (VNC) – servidor VNC com autenticação

- **Certificado SSL:**
  - Emitido por Siemens AG, família S7-1200
  - Validade: 31/12/2011 a 01/01/2042
  - CN: 192.168.1.10
  - SAN: inclui IP interno 192.168.1.10

- **Informações do PLC:**
  - Modelo: Siemens S7-1200
  - Comunicação via porta 102 resultou em timeout

- **VNC:**
  - Porta 5900 ativa com VncAuth 
  - Conexão aceita, mas falha com possível firewall

## Evidências

- Interfaces HTTP/HTTPS acessíveis publicamente
- Certificado SSL legítimo da Siemens
- Porta 102 aberta indicando exposição do protocolo industrial
- Porta VNC aberta, com proteção via senha (possivelmente fraca)
- Comunicação com PLC parcialmente possível, mas sem sucesso

## Riscos

- Ataques de força bruta e exploração via interface web
- Manipulação direta do PLC via porta 102 aberta
- Ataques via VNC se senhas forem fracas ou padrão
- Impacto grave em processos industriais e segurança operacional

## Recomendações

1. Isolar sistemas SCADA e PLC da internet pública
2. Usar VPN ou redes internas confiáveis para acesso remoto
3. Aplicar senhas fortes e autenticação multifator (MFA)
4. Manter firmware e software Siemens atualizados
5. Bloquear portas 102 e 5900 para acessos não autorizados
6. Monitorar acessos e tentativas de login continuamente

---

**Relatório por:** Whoami-a51  
**Data:** 18, Julho de 2025

