___
2026-01-22--10:30

Status: #Finish 

Tags: [[CIS]], [[Dados]], [[Governança]]
___
# Conceito Geral
### 1. Cenário e Importância

- **Fim das Fronteiras:** Os dados não estão mais presos nos servidores da empresa. Estão em nuvem (Teams, Google Drive), dispositivos pessoais e principalmente com a vinda do _home office_.
- **Volume:** Estimativa de que o volume de dados triplique (3x) nos próximos 5 anos.
- **Risco:** 96% dos líderes temem pela continuidade dos negócios pós-ataque. Violações custam milhões e afetam a reputação.
- **Legal (Brasil):**
    - **LGPD (Lei 13.709/18):** Exige medidas técnicas e administrativas para proteger dados.
    - **ANPD:** Órgão que fiscaliza e aplica multas.
    - **Art. 46:** Responsabiliza os agentes de tratamento pela segurança.


### 2. Gestão e Ciclo de Vida
Para proteger, é preciso primeiro **identificar** e **mapear**.
- **Inventário de Dados:** Saber o que a empresa tem, onde está, quem consome e como é descartado.
- **Classificação dos Dados:**
    1. **Público:** Acesso livre.
    2. **Confidencial:** Acesso restrito/permitido.
    3. **Sensível:** Se vazado, pode gerar **discriminação** (ex: religião, saúde, biometria).

### 3. Medidas Técnicas de Proteção (CIS Control 3)
O CIS recomenda 5 medidas principais para blindar os dados:
1. **Controle de Acesso (ACL):**
    - Princípio da **Necessidade de Conhecer** (só acessa quem precisa).
    - Princípio do **Privilégio Mínimo** (só dar permissão de leitura se não precisar editar) [[Jit-Just-In-Time]].
2. **Retenção e Descarte Seguro:** Definir prazos para guardar dados e métodos seguros para destruí-los (impedir recuperação).
3. **Segmentação de Rede:** Separar dados críticos do resto da rede para evitar "movimento lateral" (o hacker invadir um PC comum e chegar ao servidor principal).
    
4. **Auditoria e Monitoramento (DLP):**
    - Ferramentas de **DLP (Data Loss Prevention)** monitoram exfiltração de dados.
    - Evitar vazamentos acidentais ou maliciosos.
5. **Criptografia:** Transformar texto em cifra. Essencial para dois estados:
### 4. Criptografia na Prática

#### A. Dados em Repouso (Armazenados em HD, PenDrive, Nuvem)
- **Objetivo:** Se o dispositivo for roubado, o ladrão não lê os dados.
- **Ferramentas:**
    - **BitLocker:** Nativo do Windows (atenção ao chip TPM e chave de recuperação).
    - **FileVault:** Nativo do Mac (Apple).
    - **dm-crypt:** Para Linux.
    - **VeraCrypt:** Open source e multiplataforma.
#### B. Dados em Trânsito (Viajando pela rede/internet)
- **Objetivo:** Evitar interceptação no caminho.
- **O que usar (Seguro):** HTTPS (com TLS 1.2 ou 1.3), SFTP, SSH.
- **O que EVITAR (Obsoleto/Inseguro):** HTTP, FTP, Telnet, SSL antigo, TLS 1.0/1.1.

---

# 📚 Estudo Dirigido

_Tente responder às perguntas mentalmente antes de ler a resposta (escondida na seta ou logo abaixo)._

#### Bloco 1: Conceitos e Legislação

**1. Por que dizemos que o perímetro de segurança da empresa "desapareceu"?**

> **Resposta:** Porque os dados agora residem em dispositivos móveis, nuvem (SaaS) e computadores pessoais (home office), fora da rede física tradicional da empresa.

**2. Qual a diferença entre um Dado Confidencial e um Dado Sensível?**

> **Resposta:** O Confidencial exige acesso restrito/autorizado. O Sensível é aquele que, se vazado, pode gerar discriminação contra a pessoa (origem racial, opinião política, saúde, etc).

**3. O que determina o Artigo 46 da LGPD sobre a responsabilidade das empresas?**

> **Resposta:** Determina que os agentes de tratamento devem adotar medidas de segurança, técnicas e administrativas, aptas a proteger os dados pessoais de acessos não autorizados.

#### Bloco 2: Medidas de Segurança (CIS)

**4. O que é o princípio do "Privilégio Mínimo"?**

> **Resposta:** É a prática de conceder a um usuário apenas as permissões estritamente necessárias para realizar seu trabalho (ex: apenas ler, não apagar), reduzindo o risco em caso de invasão de conta.

**5. Para que serve a "Segmentação de Rede" na proteção de dados?**

> **Resposta:** Serve para isolar ativos críticos. Se um computador menos importante for invadido, a segmentação impede (ou dificulta) o "movimento lateral" do atacante até o banco de dados principal.

**6. Qual a função de uma solução de DLP (Data Loss Prevention)?**

> **Resposta:** Ela "escuta" e monitora o ambiente para identificar, alertar ou bloquear a transferência não autorizada de dados sensíveis/confidenciais (prevenção de vazamento).

#### Bloco 3: Ferramentas e Criptografia

**7. Associe a ferramenta ao Sistema Operacional correto:** ( A ) BitLocker ( B ) FileVault ( C ) dm-crypt

> **Resposta:** (A) Windows, (B) macOS, (C) Linux.

**8. Você precisa configurar um servidor web seguro. Quais protocolos deve ativar e quais deve desativar?**

> 	**Resposta:** HTTPS com TLS 1.2 ou 1.3  e desativar HTTP puro, SSL, TLS 1.0 e TLS 1.1 (são obsoletos).


**9. Para transferência de arquivos e acesso remoto, quais são as alternativas seguras ao FTP e Telnet?**

> **Resposta:** Deve-se usar **SFTP** (ou SCP) no lugar de FTP, e **SSH** no lugar de Telnet.

___

# Referências

1. https://www.cisecurity.org/insights/blog/how-to-create-a-data-protection-plan