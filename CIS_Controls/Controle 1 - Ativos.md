___
2026-01-07--14:36

Status: #Finish 

Tags: [[CIS]], [[Ativos]], [[Governança]]
___
# Conceito Geral

### O que é CIS Controls?
Conjunto de 18 práticas recomendadas para resolver/implementar/melhorar/fortalecer a postura de segurança cibernética em uma empresa.

#### Diferença entre os Controles 1 e 2

Controle 1: Gerenciamento de Ativos
Controle 2: Controle de Ativos de Softwares

Ativo: Qualquer dispositivo físico, virtual, conectado a organização. Podendo ser físico ou em nuvem, e não se limitando a dispositivos finais.

EX:
![[Pasted image 20260107145911.png]]


Controle de ativos e importante, pq como podemos proteger, o que não sabemos que temos?
Depois de sabermos, por onde começamos? o que é prioridade e o que não é?

# Controle 01
### Procedimentos
1. Visibilidade dos Ativos ( Que tipo de ativo, onde está, endereço na rede, nome)
2. Correlação e análise de criticidade(Permissões dos ativos)

A própria CIS disponibiliza um modelo de Planilha para a criação de um bom inventário.
https://www.cisecurity.org/insights/white-papers/cis-controls-inventory-tracking-spreadsheets
![[CIS_Controls_v8.1_Inventory_Spreadsheet.xlsx]]
##  Métodos de Inventário
Para montar o inventário do 0, cruzamos dados de três fontes principais:

### A. Active Discovery /  Domínio

- **Como funciona:** Envia pacotes para a rede e aguarda resposta dos dispositivos.
- **Ferramenta Exemplo:** **Nmap** (Zenmap).
- **Prós:** Detalhado (pega OS, portas, serviços).
- **Contras:** Intrusivo (pode gerar instabilidade ou derrubar sistemas legados/frógeis).

Para cumprir o CIS Control 01, não basta saber que o ativo existe ("está ligado"). É necessário saber **o que** ele é para gerenciar vulnerabilidades.

#### Principais Parâmetros para Inventário

| **Parâmetro** | **Nome Técnico**   | **O que faz?**                                                                              | **Quando usar?**                                                            | **Nível de Ruído**        |
| ------------- | ------------------ | ------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------- | ------------------------- |
| -sn           | Ping Scan          | Verifica apenas se o host está ativo (não escaneia portas).                                 | **Passo 1:** Para mapear rapidamente quais IPs estão em uso na rede.        | 🔇 Silencioso             |
| -sV           | Version Detection  | Interroga as portas abertas para descobrir o software e versão exata (Ex: _Apache 2.4.49_). | **Passo 2:** Essencial para cruzar com CVEs e identificar vulnerabilidades. | 🔊 Alto (Gera logs)       |
| -O            | OS Detection       | Tenta adivinhar o Sistema Operacional via análise de pacotes TCP/IP.                        | Para saber se é Windows, Linux, Impressora, etc.                            | 🔉 Médio                  |
| -sS           | SYN Scan (Stealth) | Realiza a conexão pela metade (não completa o _handshake_).                                 | Padrão de mercado para não deixar logs de acesso na aplicação alvo.         | 🔉 Baixo                  |
| -T2           | Timing (Polite)    | Reduz a velocidade da varredura.                                                            | Em redes legadas, industriais ou instáveis para evitar derrubar serviços.   | 🔇 Silencioso (mas lento) |
|               |                    |                                                                                             |                                                                             |                           |

1. Descoberta Inicial (Ping Sweep)
Objetivo: Listar IPs vivos sem tocar nas portas. Lembrando que o IP deve ser alterado para o da sua rede e máscara
```
nmap -sn 192.168.1.0/24
```

2. Inventário Detalhado (Segmentado)

```
# -sS (Stealth), -sV (Versões), -T2 (Lento/Seguro), -O (Sistema Operacional)
nmap -sS -sV -T2 -O <IP_ALVO>
```

### B. Descoberta Passiva

- **Como funciona:** Apenas "escuta" o tráfego da rede (Sniffer) sem interagir com os hosts. Geralmente via _Port Mirroring_ no Switch.
- **Ferramenta Exemplo:** **Wireshark**.
- **Prós:** Não intrusivo (invisível para o alvo), não gera instabilidade.
- **Contras:** Pode demorar mais para pegar dados se o ativo estiver silencioso.
### C. Logs de DHCP

- **Função:** O servidor DHCP registra quem entrou na rede e pediu IP.
- **Uso:** Serve como fonte da verdade para validar os dados das descobertas ativa/passiva.
- **Local (Windows):** `%systemroot%\system32\dhcp`.

##Shadow IT (TI Invisível)

**Definição:** Hardware, software ou serviços usados sem aprovação/conhecimento da TI. **Riscos:** Vulnerabilidades não corrigidas, vazamento de dados, falta de suporte. **Tratamento (O que fazer):**

1. **Identificar:** Via varredura (métodos acima).
2. **Investigar:** É malicioso ou necessidade de negócio?
3. **Ação:** Remover da rede, negar acesso (Bloqueio/NAC) ou colocar em quarentena.


___

# Referências

1. https://www.cisecurity.org/insights/white-papers/cis-controls-inventory-tracking-spreadsheets