___
2026-01-22--16:42

Status: #Developing 

Tags: [[CIS]], [[Governança]], [[Ativos]], [[Software]]
___
# Conceito Geral
 ### O Problema: "Configuração de Fábrica"
- **O Risco:** Equipamentos e softwares vêm com configurações padrão para facilitar a instalação (plug-and-play), mas são inseguras.
- **Vulnerabilidades Comuns:**
    - Senhas padrão (_admin/admin_, _root_).
    - Portas e serviços desnecessários abertos.
    - Alguns Protocolos obsoletos.
- **Exemplo:** **Botnet Mirai (2016)**. Infectou 400.000 dispositivos IoT usando senhas de fábrica e derrubou Twitter e Netflix via ataque DDoS.
- **OWASP Top 10:** Classifica "Configuração Incorreta de Segurança" como um dos riscos mais críticos em aplicações web.
### Conceitos Chave
- **Baseline de Segurança (Hardening):** É o "piso" de segurança. Um conjunto documentado de configurações mínimas que devem ser aplicadas a todos os dispositivos (ex: desativar porta X, exigir senha Y).
    - _Fontes:_ CIS Benchmarks, Microsoft Security Compliance Toolkit.
- **Infrastructure as Code (IaC):** Gerenciar configurações via código/script (versionado). Garante que a instalação seja rápida, consistente e sem "erro humano". Evita configuração manual.
- **Ciclo de Vida:** A configuração não é feita uma única vez. Deve ser reavaliada continuamente para evitar degradação da segurança após atualizações.
### 3. Medidas Técnicas de Proteção (CIS Control 4)
O CIS recomenda ações específicas para "endurecer" (_harden_) o ambiente:
#### A. Gestão de Acesso e Bloqueio
- **Bloqueio Automático (Inatividade):** Evita ameaça interna (alguém usar seu PC quando você vai ao banheiro).
    - _Tempo recomendado:_ Até **15 min** (Geral) e **2 min** (Dispositivos Móveis).
- **Bloqueio por Tentativa (Força Bruta):** Bloquear o dispositivo após X tentativas de senha errada.
- **Gestão de Contas:**
    - Remover/Desativar contas padrão.
    - Não usar nomes óbvios (_user_admin_).
    - Separar contas de administração das contas de uso diário (navegação).

#### B. Proteção de Rede e Serviços
- **Firewall Local (Host-based):** Instalar firewall no próprio computador/servidor para bloquear portas desnecessárias.
- **DNS Confiável:** Não usar o DNS padrão do provedor se não for seguro. Usar DNS interno ou externos confiáveis (Google 8.8.8.8, Cloudflare 1.1.1.1) para evitar **DNS Poisoning** (redirecionamento para sites falsos).
- **Protocolos Seguros:** Usar **SSH** e **HTTPS** para gestão.
#### C. Dispositivos Móveis (Mobile)
- **Remote Wipe (Limpeza Remota):** Capacidade de apagar dados do celular roubado/perdido sem acesso físico.
- **Separação de Espaços de Trabalho:** Criar um "container" no celular. Se o usuário pegar um vírus no perfil pessoal, não afeta os dados corporativos.

### 4. Ferramentas e Soluções
- **MDM (Mobile Device Management):** Gerencia celulares remotamente.
    - _Exemplos:_ Microsoft Intune, Apple Configuration Profile, Android Work Profile.
- **SCAP (Security Content Automation Protocol):** Ferramentas para verificar se os ativos estão seguindo a _Baseline_.
    - _Exemplos:_ **SCC** (Naval Information Warfare Center), **CIS-CAT Lite** (Gratuita, mas limitada).

---

# 📚 Estudo Dirigido (Controle 4)

_Tente responder mentalmente antes de conferir a resposta._

#### Bloco 1: O Risco e o Processo

**1. Por que manter as configurações de fábrica (padrão) é considerado um risco grave?**

> **Resposta:** Porque elas priorizam a facilidade de uso em detrimento da segurança, frequentemente mantendo senhas públicas (admin/admin), serviços desnecessários ativos e protocolos obsoletos conhecidos por atacantes (Botnet Mirai).

**2. O que é uma "Baseline de Segurança" ou "Hardening"?**

> **Resposta:** É um conjunto documentado de configurações mínimas de segurança (ex: parâmetros de registro, portas fechadas, políticas de senha) que servem como ponto de partida obrigatório para qualquer novo ativo na rede.

**3. Como a "Infraestrutura como Código" (IaC) ajuda na segurança?**

> **Resposta:** Ela padroniza a configuração através de scripts. Isso evita erros manuais humanos, garante consistência (todos os servidores ficam iguais) e permite controle de versão (saber quem mudou o que e quando).

#### Bloco 2: Medidas Técnicas

**4. Qual o tempo máximo de inatividade recomendado pelo CIS para bloqueio de tela em estações de trabalho e dispositivos móveis?**

> **Resposta:** 15 minutos para estações de trabalho (geral) e 2 minutos para dispositivos móveis.

**5. Por que é recomendado usar servidores DNS confiáveis (como Google ou Cloudflare) em vez de qualquer um?**

> **Resposta:** Para evitar ataques de _DNS Poisoning_ ou _Hijacking_, onde um servidor DNS comprometido redireciona o usuário de um site legítimo para um site falso/malicioso para roubar dados.

**6. O que é a técnica de "Separação de Espaços de Trabalho" em dispositivos móveis?**

> **Resposta:** É a criação de perfis distintos no mesmo aparelho (Pessoal vs. Corporativo), isolando os dados e aplicativos da empresa. Se o lado pessoal for comprometido, o lado corporativo permanece seguro.

#### Bloco 3: Ferramentas

**7. O que é uma solução de MDM e para que serve o recurso "Remote Wipe"?**

> **Resposta:** MDM (_Mobile Device Management_) gerencia dispositivos móveis. O _Remote Wipe_ permite que a empresa apague remotamente todos os dados corporativos de um dispositivo em caso de perda ou roubo.

**8. Cite uma ferramenta mencionada no texto capaz de verificar a conformidade com baselines de segurança (SCAP).**

> **Resposta:** CIS-CAT Lite ou SCC (da NIWC).


___

# Referências
1. BRASIL. Ministério da Gestão e da Inovação em Serviços Públicos (MGI). **Guia do Framework de Privacidade e Segurança da Informação**. Programa de Privacidade e Segurança da Informação (PPSI). versão 1.1.2. Brasília, DF: SGD, 2023. Disponível em: [https://www.gov.br/governodigital/pt-br/seguranca-e-protecao-de-dados/ppsi/guia_framework_psi.pdf(opens in a new tab)](https://www.gov.br/governodigital/pt-br/seguranca-e-protecao-de-dados/ppsi/guia_framework_psi.pdf). Acesso em: 2 out. 2023.
2. CENTER FOR INTERNET SECURITY (CIS). **CIS Controls v8**. [_S. l._]: CIS, 2021. Disponível em: [https://www.cisecurity.org/controls/v8/(opens in a new tab)](https://www.cisecurity.org/controls/v8/). Acesso em: 25 jul. 2023.
3. CENTER FOR INTERNET SECURITY (CIS). **Essential Guide to Election Security**. [_S. l._]: CIS, 2023. Disponível em: [https://essentialguide.docs.cisecurity.org/en/latest/index.html(opens in a new tab)](https://essentialguide.docs.cisecurity.org/en/latest/index.html). Acesso em: 25 jul. 2023.
4.  CENTER FOR INTERNET SECURITY (CIS). How to Create a Data Protection Plan. **CIS**, [_s. l._], [_s. d._]. Disponível em: [https://www.cisecurity.org/insights/blog/how-to-create-a-data-protection-plan(opens in a new tab)](https://www.cisecurity.org/insights/blog/how-to-create-a-data-protection-plan). Acesso em: 2 out. 2023.
5.  MARZANO, A. et al. The Evolution of Bashlite and Mirai IoT Botnets. In: IEEE Symposium on Computers and Communications (ISCC), 2018, Natal. **Proceedings** [...] Natal, Brazil: IEEE, 2018. p. 813-818. Disponível em: [https://ieeexplore.ieee.org/document/8538636(opens in a new tab)](https://ieeexplore.ieee.org/document/8538636). Acesso em: 25 jul. 2023.
6.  OWASP. OWASP Top Tem. [_S. l._]: **Owasp**, 2021. Disponível em: [https://owasp.org/www-project-top-ten(opens in a new tab)](https://owasp.org/www-project-top-ten)[/(opens in a new tab)](http:). Acesso em: 25 jul. 2023.