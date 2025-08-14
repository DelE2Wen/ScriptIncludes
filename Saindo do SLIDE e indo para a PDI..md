User: Dominique Santiago

**O Desafio de Dominique Santiago na BubbleIT**

**Personagem:** Dominique Santiago, uma talentosa consultora ServiceNow da BubbleIT.
**Cliente:** Uma empresa de médio porte que está lutando para organizar seus processos de solicitação de TI.
**Cenário:** Dominique chega ao cliente e encontra um processo de solicitação de software confuso. Eles têm um item de catálogo, mas a lógica de atribuição de aprovação está espalhada e duplicada, causando inconsistências. Além disso, os usuários só descobrem o custo do software depois de enviar a solicitação, gerando cancelamentos e retrabalho.

Dominique sorri. "Temos uma oportunidade clara aqui para centralizar a lógica, melhorar a manutenção e a experiência do usuário. Vamos usar um Script Include."


#### **Passo 1: Criando o Ambiente (O Setup de Dominique)**

**Story:** "Antes de tudo, Dominique sabe que um bom trabalho começa com uma boa organização. Ela não vai poluir o escopo Global. Ela criará uma pequena aplicação para abrigar todas as suas melhorias. Isso garantirá que seu trabalho seja organizado, seguro e fácil de migrar entre instâncias."

Criada uma aplicação que conterá toda a automação necessária

Entra no escopo da aplicação
Criado os grupos: "Design", "Engenharia e "ServiceDesk"
e começa a criar seus scripts.

Criando Script Include
![[Pasted image 20250813200034.png]]
na hora de salvar é pedido uma role que poderá acessar, pois chamadas para o servidor devem ser protegidas por ACL.
Aqui foi selecionada ITIL

#### **Passo 2: O Problema - A Lógica Duplicada (O Diagnóstico de Dominique)**

**Story:** "Dominique investiga e encontra duas Business Rules que fazem quase a mesma coisa. Uma roda na tabela de Requisição (`sc_request`) e outra na tabela de Item Requisitado (`sc_req_item`). Ambas tentam definir o grupo de aprovação para solicitações de software, mas com lógicas ligeiramente diferentes. Se a lógica de aprovação mudar, o administrador precisa se lembrar de atualizar os dois locais. É uma armadilha de manutenção."

//vou deixar na PDI

Destaque como os `sys_id`s estão "hardcoded" e a lógica está em dois lugares diferentes.

vá em **System Definition > Script Includes**.

Abra o script BubbleITUtils
Explique o código rapidamente
e fale como os grupos não estão hardcoded e que é boa prática

## Hora da Refatoração de Dominique

**Story:** "Agora, com a lógica centralizada, Dominique pode desativar as antigas Business Rules e criar uma única, nova e limpa Business Rule que simplesmente chama seu Script Include. O código se torna uma única linha, fácil de ler e manter."

System Definition > Business Rules.
    BubbleIT - Definir Aprovação para Software
    abra e explique rapidamente o código e o chamado para script include
diga que a clareza é a maior vantagem. Se a lógica de aprovação mudar, você só mexe no Script Include, e este BR continuará funcionando perfeitamente.


## **Melhorando a Experiência do Usuário com GlideAjax**

**Story:** "Dominique não para na otimização do backend. Ela quer resolver o problema do custo do software. Usando a mesma Script Include, ela vai fazer com que o formulário de solicitação mostre o custo em tempo real, assim que o usuário selecionar um software. Chega de surpresas!"

**Service Catalog > Catalog Definitions > Maintain Items**.
fale que criou o **Solicitação de Licença de Software**

Em listas relacionadas clique em client script e terá o BubbleIT - Atualizar Custo do Software
fale desse client script e fale de onde vem os valores **SEMPRE FOCANDO no script include, por favor.**

Sobre o script include e o client-side:
	no fim, puxe novamente dizendo que é uma API que modifica o client-side, mas tudo roda no server-side


- Vá para o seu item de catálogo (clique em "Try It").
    
- Selecione "photoshop" no select box. O campo de custo deve ser preenchido com "250.00".
    
- Selecione "visio". O custo deve mudar para "150.00".
    
- Preencha os outros campos e envie a solicitação.
    
- Abra o RITM (Requested Item) gerado e verifique se o campo "Approval Group" foi definido corretamente pela sua Business Rule.

fale que o assign_to está vazio, pois está definido para mostrar nos grupos e lá um usuário se inscrever nessa tarefa, pois a primeira responsabilidade da automação é garantir que a tarefa chegue à **fila da equipa correta** e o `assigned_to` só é preenchido quando um **membro individual da equipa assume a responsabilidade** por aquela tarefa específica. Isto é uma ação manual e consciente.

Se for automático:
- E se o João estiver de férias? O pedido ficará parado uma semana.
    
- E se o João estiver doente? O pedido não será atendido.
    
- E se o João já tiver 50 tarefas e a "Maria" não tiver nenhuma? A sua automação estaria a criar um desequilíbrio na carga de trabalho.
- 
  
## Volte para o SLIDE:

Então, deve estar para membros disponíveis selecionarem.
Onde pode encontrar? Em my groups works lá no SOW (mas não precisa demonstrar, deixarei de print).
### **Conclusão para a sua Apresenttação e amarra a historia**

**Story:** "Ao final, Dominique apresentou sua solução. Ela não apenas resolveu o problema inicial de redundância de código, mas também melhorou a experiência do usuário final e tornou o sistema inteiro mais robusto e fácil de manter. O cliente ficou impressionado, e Dominique demonstrou o poder de um bom design de script no ServiceNow."