___
2026-01-23--08:34

Status: #Draft

Tags: [[CIS]], [[Governança]], [[Gerenciamento]], [[MFA]], [[RBAC]], 
___
# Conceito Geral

### Cenário e Justificativa (Por que controlar?)
- **Erro :** Organizações concedem privilégios excessivos por "conveniência" (é mais fácil dar acesso total do que configurar granularmente). Assim aumentando o risco: se essa conta for comprometida, o dano é total.
- **Dados de Impacto (IDSA 2023):**
    - 90% das organizações sofreram violação de identidade.
    - **MFA (Múltiplo Fator de Autenticação)** poderia ter evitado ou minimizado 42% desses incidentes.
- **Vetores de Ataque:** Roubo de credenciais é a causa nº 1 de violações em aplicações web. Ataques de Phishing estão cada vez mais focados em roubar logins e dados importantes.
    
### Conceitos Fundamentais
1. **RBAC (Role Based Access Control):** Conceder acesso com base na _função/cargo_ (ex: "Analistas de RH" têm acesso X) (Cria um padrão para cada cargo)
2. **Privilégio Mínimo (Least Privilege):** O usuário só deve ter o acesso estritamente necessário para fazer seu trabalho. Nada a mais.
3. **Necessidade de Saber (Need-to-Know):** Mesmo que você _possa_ tecnicamente acessar um dado, você só deve acessá-lo se for necessário para uma tarefa específica.
4. **Segregação de Funções (SoD - Segregation of Duties):** Ninguém deve ter poder suficiente para realizar uma fraude sozinho (ex: quem _solicita_ o pagamento não pode ser quem _aprova_ o pagamento).

### Medidas Técnicas de Proteção (CIS Control 6)
O CIS recomenda a automatização e a centralização para evitar o erro humano na gestão de acessos.
#### A. Centralização (SSO)
- **SSO (Single Sign-On):** Permite que o usuário faça login uma única vez para acessar vários sistemas.
- **Benefício:** Reduz o número de senhas que o usuário precisa decorar (e escrever em post-its) e permite revogar o acesso a _tudo_ de uma só vez centralmente.
#### B. MFA Obrigatório
- **Onde aplicar:** Sistemas expostos à internet, acessos remotos e contas administrativas.
- **Tipos de MFA:**
    - _Padrão:_ App autenticador (Google/Microsoft Authenticator).
    - _Resistente a Phishing (FIDO2/WebAuthn):_ Chaves físicas ou biometria que não podem ser enganadas por sites falsos (CISA recomenda fortemente para arquitetura Zero Trust).
#### C. Proteção de Acesso Administrativo (PAM & Jump Box)
- **Jump Box (Jump Server):** Um servidor intermediário "blindado". O administrador conecta primeiro nele, e dele conecta nos servidores críticos. É um ponto único de controle e auditoria.
- **PAM (Privileged Access Management):** Soluções que monitoram, gravam e controlam o uso de contas de administrador (cofre de senhas, gravação de sessão).
#### D. Gestão do Ciclo de Vida (JML - Joiners, Movers, Leavers)
- **Joiners (Entrada):** Automatizar a criação de conta baseada no RH.
- **Movers (Movimentação):** Se a pessoa muda de área, os acessos antigos devem ser revogados.
- **Leavers (Saída):** Desligamento deve disparar bloqueio imediato.
    
### Tendências
- **Zero Trust (Confiança Zero):** "Nunca confie, sempre verifique". A rede interna não é mais confiável. Cada acesso deve ser validado (Identidade + Dispositivo).
- **Passwordless:** Eliminar senhas em favor de biometria ou chaves de segurança (FIDO), reduzindo o risco de phishing e reutilização de senhas.
- **Segurança de API:** Credenciais "hardcoded" (fixas no código) são um risco enorme. APIs devem usar tokens seguros e gestão de segredos, não senhas em texto puro.

---

# 📚 Estudo Dirigido (Controle 6)

#### Bloco 1: Estratégia de Acesso

**1. O que é o conceito de "Privilégio Mínimo"?**

> **Resposta:** É garantir que o usuário tenha apenas as permissões estritamente necessárias para sua função, reduzindo o impacto caso a conta seja comprometida.

**2. Qual a diferença entre SSO e MFA?**

> **Resposta:**
> 
> - **SSO (Single Sign-On):** Centraliza o login (entra uma vez, acessa tudo). Foca em conveniência e gestão centralizada.
>     
> - **MFA (Multi-Factor Authentication):** Adiciona camadas de segurança (senha + token). Foca em validar a identidade.
>     
> - _Ideal:_ Usar os dois juntos.
>     

**3. O que é uma "Jump Box" e para que serve?**

![[Pasted image 20260123090629.png]]

> **Resposta:** É um servidor seguro intermediário usado obrigatoriamente por administradores para acessar ambientes críticos. Serve para isolar o acesso administrativo e facilitar a auditoria.

#### Bloco 2: Riscos Modernos

**4. Por que a CISA recomenda o "MFA Resistente a Phishing"?**

> **Resposta:** Porque atacantes já conseguem enganar usuários para entregarem códigos de MFA simples (via sites falsos). O MFA resistente (como chaves FIDO) valida o domínio do site, impedindo esse ataque.

**5. O que significa "Zero Trust"?**

> **Resposta:** O modelo de segurança que assume que nenhuma conexão é confiável por padrão, mesmo dentro da rede da empresa. Exige verificação contínua de identidade e contexto para cada acesso.

**6. Qual o risco de credenciais em APIs ("Hardcoded")?**

> **Resposta:** Se um desenvolvedor deixa uma senha fixa no código, qualquer pessoa que tiver acesso ao código (ou engenharia reversa do app) terá acesso total ao sistema/banco de dados conectado.


___

# Referências