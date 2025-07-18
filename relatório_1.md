Relatório de Invasão 1 — Acesso Remoto a Sistema Industrial via VNC

🧠 Contexto

Durante uma varredura passiva utilizando o Shodan, identificamos múltiplos hosts industriais expostos na internet com portas e serviços potencialmente inseguros — entre eles, sistemas SCADA com acesso remoto habilitado via VNC sem autenticação.

Esses dispositivos estavam relacionados a controladores de turbinas industriais e sistemas de automação crítica.

🔍 Fase de Reconhecimento

Ferramenta utilizada:

Shodan

Query usada:

port:5900 has_screenshot:true

Essa query retorna instâncias de VNC com tela acessível (screenshot) — o que muitas vezes indica ausência de autenticação.

Observações:

Host localizado em rede industrial (ASN confirmada de energia ou manufatura).

VNC com autenticação desabilitada (authentication disabled no banner).

Visualização direta da interface SCADA (monitoramento de turbinas, pressão e temperatura).

Sistema operando em tempo real.

🎯 Acesso Remoto

Utilizamos o VNC Viewer para conexão direta à interface remota:

vncviewer <IP>:5900

O acesso foi concedido sem solicitação de senha, possibilitando interação direta com a HMI (Interface Homem-Máquina) da turbina.

🛠️ Capacidade de Controle

Dentro da interface observada, foi possível:

Alterar parâmetros de rotação e carga

Iniciar ou parar turbinas

Modificar valores de setpoint

Visualizar alarmes e eventos críticos

⚠️ Nota: Nenhuma alteração real foi feita no sistema. A exploração foi puramente observacional e ética.

🢨 Perigos e Impacto

Esse tipo de exposição representa risco extremo à infraestrutura crítica. Um invasor poderia:

Paralisar uma linha de produção

Causar sobrecarga em turbinas, gerando dano físico

Iniciar acidentes operacionais com risco humano

Sabotar remotamente uma instalação energética

🚒 Mitigações Recomendadas

Desabilitar acesso VNC público

Exigir autenticação robusta (com senha forte ou chave)

Isolar redes industriais (air gap ou firewall)

Utilizar VPN com autenticação para acesso remoto

Monitorar tráfego e implementar SIEM

📎 Evidências (anonimizadas)

IP parcialmente ocultado: xxx.xxx.121.84

ASN: ISP de energia regional

Screenshot ofuscado salvo em: /evidencias/vnc_turbina_01.png

🧪 Ferramentas Envolvidas

shodan.io

vncviewer (RealVNC)

whois, nmap para enriquecimento

✅ Conclusão

Esse caso mostra como sistemas industriais expostos sem autenticação mínima representam risco nacional. A facilidade com que um invasor pode assumir controle de turbinas reforça a necessidade urgente de revisão das políticas de segurança OT/ICS (Operational Technology / Industrial Control Systems).

Relatório gerado para fins educacionais e de conscientização em cibersegurança industrial.

