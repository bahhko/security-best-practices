---
📄 Documento: Boas Práticas de Endpoints
📅 Versão: 1.0
👤 Autor: Bruno Atilio
🏷️ Categoria: Segurança Operacional / Blue Team
---

# Boas Práticas de Segurança em EndPoints (Windows e Linux)
## 1. OBJETIVO
Definir diretrizes e recomendações de segurança para proteger endpoints(Estações de trabalho Windows ou Linux), garantindo confidencialidade, integridade e disponibilidade das informações.

## 2. ESCOPO
Aplica-se a todos os dispositivos corporativos ou pessoais.

## 3. CONCEITOS E DEFINIÇÕES
 -  Endpoint: Qualquer dispositivo que se conecta a rede(Notebook, servidor, desktop, etc);
 -  Hardening: Processo de identificação e mitigação de erros e ameaças;
 -  EDR: (Endpoint Detection and Response) ferramenta de detecção e resposta em endpoints;
 -  Patch: Atualização de segurança que corrige uma vulnerabilidade conhecida;
 -  BL(BitLocker): Recurso de criptografia do Windows que protege seus dados.
 -  GP(Group Policy): Permite os admins. de rede gerenciar e controlar configurações de usuários.
 -  Path: Variável de ambiente
 -  Rainbow Tables: Banco de dados de senhas já catalogadas/descobertas

## 4. CONTROLES DE SEGURANÇA
4.1. Manter o dispositivo sempre atualizado.
  - Habilitar atualizações automáticas, Windows Update e Linux ´unattended-upgrades´.
  - Aplicar patches de segurança críticos em até 15 dias após lançamento (CIS Control 7).

4.2. Manter o dispositivo sempre atualizado.
  - Habilitar atualizações automáticas, Windows Update e Linux ´unattended-upgrades´.
  - Aplicar patches de segurança críticos em até 15 dias após lançamento (CIS Control 7).

4.3. Definir boa política de senha
  4.3.1. - Definir um número de histórico de senha de 24(ou mais, se o sistema permitir), garantindo que nenhuma das últimas 24 ou X senhas sejam reaproveitadas.
  
   > [!IMPORTANT] 
   > Justificativa: Quanto mais tempo com a mesma senha, maior a chance de um atacante descobrir a senha por meio de ataques de força bruta.

   > [!TIP] 
   > defina o seguinte caminho de interface de usuário para 24 ou mais senhas:
   > ´Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Password Policy\Enforce password history´

  4.3.2.- Definir política de expiração de senha(Até 365 dias, mas nunca 0), Padrão: 42 dias de validade.
   > [!IMPORTANT] 
   > Justificativa: Quanto menor o tempo de duração de uma senha, maior a dificuldade para o invasor, porém, consequentemente pode aumentar os chamados para o suporte técnico, devido a necessidade de alteração de senha, ou esquecimento da mesma.

   > [!TIP] 
   > Para definir via GP, siga o caminho de GPO:
   > ´Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Password Policy\Maximum password age´

  4.3.3.- Definir o número de dias que se deve usar a senha antes de altera-la, sendo 1 ou mais dias o recomendado.
   > [!IMPORTANT]
   > Justificativa: Impede que o usuário fique alterando a senha repetidamente em um curto período de tempo, tentando contornar a política acima de histórico de senha.

   > [!TIP] 
   > Para definir a configuração via GP, siga o caminho de GPO:
   > ´Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Password Policy\Minimum password age´

 4.3.4.- Definir o tamanho minímo de senha, recomendado 14 caracteres ou mais(Muitas empresas utilizam no mínimo 8 caracteres).
   > [!IMPORTANT]
   > Justificativa: Impede o uso de senhas fracas pelo usuário, dificultando assim o acesso de invasores e o descobrimento das senhas fracas já catalogadas em rainbow tables.

   > [!TIP] 
   > Para definir a configuração via GP, siga o caminho de GPO:
   > ´Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Password Policy\Minimum password length´

4.3.5.- Definir a complexidade de senha(se deve conter maiusculas, minusculas, números, caracteres especiais) e requisitos.
   > [!IMPORTANT]
   > Justificativa: Do que adianta todos o nosso trabalho anterios, se o usuário por exemplo pode colocar senhas como "12345678", "empresa2025"?, o aumento de complexidade e requerimentos obriga o usuário a atender os requisitos minímos de criação de senha, além de não poder repetir as ultimas X senhas, ter no mínimo 8 caracteres, não poder troca-la em 1 dia, e etc. Tudo isso faz com que nossas senhas sejam cada vez mais rigorosas e acertivas dentro da área da segurança da informação.

   > [!TIP] 
   > Para definir a configuração via GP, siga o caminho de GPO:
   > ´Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Password Policy\Minimum password length´
     
