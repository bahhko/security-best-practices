___
2026-01-22--17:07

Status: #Finish 

Tags: [[CIS]], [[Governança]], [[IAM]], [[MFA]]
___
# Conceito Geral
### Cenário e Riscos

- **Problema:** Contas "zumbis" (de ex-funcionários), contas de teste esquecidas, contas de serviços não utilizadas, senhas compartilhadas e credenciais "hardcoded" (embutidas no código) são portas abertas pra atacantes.
- **Dados Reais:**
    - **ChatGPT:** 100 mil contas comprometidas estão à venda na Dark Web (Brasil é um dos mais afetados).
    - **Ataques Web:** 86% das violações em Aplicações Web acontecem via credenciais roubadas (Verizon DBIR 2023).
        
- **O Alvo Principal:** Contas **Administrativas/Privilegiadas**.
### Gestão (Visibilidade)
- **Regra de Ouro:** "Visibilidade, Visibilidade, Visibilidade". Não podemos proteger o que não sabemos que existe.
- **Inventário de Contas:** Assim como hardware e software, é preciso inventariar _quem_ tem acesso. O inventário deve ter:
    - Login, Proprietário, Departamento.
    - Nível de privilégio (Admin ou Comum).
    - Data de revisão.
- **Revisão Periódica:** Validar se a conta ainda deve existir (principalmente após demissões ou fim de projetos).
###  Medidas Técnicas de Proteção (CIS Control 5)
#### Senhas Fortes (Medida 5.2)

- **Complexidade:** Senhas longas e únicas.
- **MFA (Múltiplo Fator):** Senha forte sozinha não basta. O MFA (código no celular/email) é essencial, especialmente para Admins.
- **Hive Systems Table:** Mostra que senhas complexas que antes demoravam para ser quebradas agora caem mais rápido com ajuda de IA/Hardware moderno.
    - _Recomendação CIS:_ Mínimo de **8 caracteres** (com MFA) ou **14 caracteres** (sem MFA).
#### Desabilitar Contas Inativas
- **Ação:** Desativar ou excluir contas sem uso.
- **Prazo Recomendado:** Após **45 dias** de inatividade.
- **Atenção Legal:** Às vezes não se pode _excluir_ (apagar do banco) por questões de auditoria/lei, apenas _desabilitar_ (inutilizar).
#### Restringir Privilégios (Medida 5.4)
- **O Erro Comum:** Usar a conta de "Admin" para ler e-mail e navegar na internet. Se clicarmos num link malicioso como Admin, o vírus ganha poder total.
- **Boas Práticas:**
    - Usar conta comum para o dia a dia.
    - Usar conta Admin <span style="background:#fff88f">apenas</span> para configurar o sistema.
    - NCSC (Nova Zelândia) diz que restringir admin é uma das 4 estratégias mais vitais de segurança.

#### Centralização (Medida 5.6)
- **Evitar Contas Locais:** Não criar usuários soltos em cada máquina.
- **Usar Diretório:** Centralizar tudo no **Active Directory (AD)** ou **LDAP**. Isso permite bloquear um usuário demitido com um único clique, em vez de ir máquina por máquina.


### 4. Conceitos Importantes
- **IAM (Identity and Access Management):** Soluções que garantem que a pessoa certa acesse o recurso certo na hora certa.
- **Elevação de Privilégio:** Técnica de ataque onde o hacker entra como "usuário comum" e explora uma falha para virar "Admin".
- **Cofre de Senhas (Password Manager):** Ferramenta para gerenciar senhas complexas e únicas sem precisar decorar todas.

---

# 📚 Estudo Dirigido (Controle 5)

#### Bloco 1: Riscos e Senhas

**1. Segundo o relatório da Verizon (2023), qual é a causa de 86% das violações em aplicações web?**

> **Resposta:** Uso de credenciais roubadas.

**2. O que o estudo da Hive Systems (2023) revelou sobre a quebra de senhas com o uso de IA (ChatGPT)?**

> **Resposta:** Que o tempo necessário para quebrar senhas complexas caiu consideravelmente, tornando senhas antigas "fortes" mais vulneráveis.

**3. Qual a recomendação de tamanho de senha do CIS para contas COM e SEM Múltiplo Fator de Autenticação (MFA)?**

> **Resposta:** Mínimo de 8 caracteres (com MFA) e 14 caracteres (sem MFA).

#### Bloco 2: Gestão e Privilégios

**4. Após quanto tempo de inatividade o CIS recomenda desativar uma conta?**

> **Resposta:** 45 dias.

**5. Por que não devemos usar contas de Administrador para ler e-mails ou navegar na internet?**

> **Resposta:** Porque se o usuário clicar em um link malicioso (phishing) ou baixar um malware, a praga será executada com privilégios totais, podendo comprometer todo o sistema. O uso de admin deve ser restrito a tarefas de configuração.

**6. Qual a vantagem de centralizar a gestão de contas (AD/LDAP) em vez de usar contas locais?**

> **Resposta:** Facilita a gestão, monitoramento e revogação de acesso. Permite bloquear um usuário em toda a rede instantaneamente, sem precisar acessar dispositivo por dispositivo.

___

# Referências

1. HIVE SYSTEMS. Password-table. **Hive Systems**, 2023. Disponível em: [https://www.hivesystems.io/password(opens in a new tab)](https://www.hivesystems.io/password). Acesso em: 28 jul. 2023.
2. MICROSOFT. Contas atraentes para roubo de credenciais. **Microsoft**, [_s. l._], 2023. Disponível em: [https://learn.microsoft.com/pt-br/windows-server/identity/ad-ds/plan/security-best-practices/attractive-accounts-for-credential-theft(opens in a new tab)](https://learn.microsoft.com/pt-br/windows-server/identity/ad-ds/plan/security-best-practices/attractive-accounts-for-credential-theft). Acesso em: 28 jul. 2023.
3. NATIONAL CYBER SECURITY CENTRE (NCSC). **Restricting Administrative Privileges Explained**. Disponível em: [https://www.ncsc.govt.nz/assets/NCSC-Documents/NCSC-Restricting-Admin-Priviledges-Explained.pdf(opens in a new tab)](https://www.ncsc.govt.nz/assets/NCSC-Documents/NCSC-Restricting-Admin-Priviledges-Explained.pdf). Acesso em: 28 jul. 2023.
4. SHESTAKOV, D. Group-IB Discovers 100K+ Compromised ChatGPT **Accounts on Dark Web Marketplaces**; **Asia-Pacific region tops the list**. 2023. Disponível em: [https://www.group-ib.com/media-center/press-releases/stealers-chatgpt-credentials/(opens in a new tab)](https://www.group-ib.com/media-center/press-releases/stealers-chatgpt-credentials/). Acesso em: 28 jul. 2023.
5.  VERIZON. 2023 **Data Breach Investigations Report (DBIR)**. Disponível em: [https://www.verizon.com/business/resources/reports/2023-data-breach-investigations-report-dbir.pdf(opens in a new tab)](https://www.verizon.com/business/resources/reports/2023-data-breach-investigations-report-dbir.pdf). Acesso em: 28 jul. 2023.