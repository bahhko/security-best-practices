___
2026-01-09--10:38

Status: #Developing 

Tags: [[CIS]], [[Ativos]], [[Governança]], [[Software]]
___
# Conceito Geral

<span style="background:#fff88f">1. Revisar Semestralmente ou com mais frequência</span>
<span style="background:#fff88f">2. Identificar softwares pertencentes e autorizados</span>

Como já vimos anteriormente, o <u>Controle 2 </u>se trata sobre o controle e <font color="#548dd4">gerenciamento de Ativos de Software</font>s podendo ser <span style="background:#fff88f">Aplicativos ou Sistemas operacionais</span>, assim como na imagem a seguir:

![[Pasted image 20260109104131.png]]

O inventário de Software a é a maneira mais correta de listar todos os programas utilizados, para que possamos identificar e lidar com possíveis ataques, acontecendo eles por meio de softwares desatualizados causados por patches antigos ou os famosos [[Zero Day]], além de listar possíveis softwares não permitidos/ que infrinjam a política da empresa ou do time de TI. 
Para listar, antes precisamos entender que existem diferentes tipos/categorias de softwares, e dentre elas estão:

### Definições de Softwares
#### 1. Softwares Livres
Softwares livres são aqueles 777, podem ser usados, alterados, copiados, estudados, tudo isso sem nenhuma restrição, é possível vender, mas o comprador pode fazer tudo que já foi listado

#### 2. Freeware ou Software Gratuito
Livre para todos, mas não sendo possível modifica-lo

#### 3. Codigo Aberto(Open Source)
Todos tem acesso ao código, mas o que pode ou não ser feito com ele, depende de seu desenvolvedor

#### 4. ShareWare
Software com permissão para redistribuir cópias, mas diz que qualquer um que continue usando uma cópia é obrigado a pagar por uma licença. Geralmente, possui algum tipo de limitação até que seja adquirida uma licença.

#### 5. Software Privado

Sem binário ou código fonte disponíveis. 


Para realizar a coleta, é importante detalhar e registrar o Título, Fabricante, Data de Instalação, Versão, objetivo de negócio, caso tenha, endereços de internet (URL), em qual dispositivo está instalado, quem é o responsável pelo software, entre outros.


## Medidas de composição para inventário

1. Utilizar ferramentas automatizadas
2. Fazer uso de lista de permissões de software, bibliotecas e scripts autorizados
3. Identificar softwares não autorizados e realize o tratamento, sendo eles 2 tipos
	a. Softwares não suportados: Aqueles que não recebem mais atualizações devido a descontinuação do produto
	b. Softwares não autorizados: Qualquer software que leve um risco de segurança a organização


## Como Criar um Inventário de Software

1. PowerShell
2. Spiceworks - https://www.spiceworks.com/free-pc-network-inventory-software/
3. OpenAudIT - https://www.open-audit.org/

### Lista de Permissões
AppLocker é uma ferramenta incluída nos sistemas operacionais Windows e que possibilita a criação de regras para permitir ou negar a execução de softwares, podendo ser configurada também por meio de políticas de grupo (GPO – _Group Policy Object_).
___

# Referências

1. https://cdn.evg.gov.br/cursos/1073_EVG/scorms/modulo01_scorm01/scormcontent/index.html#/lessons/q165pw3qkaX9cAcf1OB9EqA1Fspdl6cI
2. https://www.spiceworks.com/free-pc-network-inventory-software/
3. https://www.open-audit.org/