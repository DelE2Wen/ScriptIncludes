<img width="433" height="209" alt="Pasted image 20250808151158" src="https://github.com/user-attachments/assets/c4ad230d-ea26-4f9a-bd0a-a0534c1ce825" />

visão geral:
	O que o script include faz?
		<img width="1844" height="872" alt="Pasted image 20250808152929" src="https://github.com/user-attachments/assets/bd46ea1e-f5d5-439d-ad73-d1a768f7e36a" />
		Por poder ser chamado via client e server, ele pode ser ambos.
		Demo:
			Chamar o SI via client-side
			nesse momento reforçar ele como uma função js
			mostrar anatomia
			Chamar via server-side
		Normalmente todos os outros tipos de scripts no servicenow possuem um trigger, na verdade, ele depende do trigger de outro Script
			// Mostrar o trigger de outro script que chama o SI
		Lembrando que por ser chamado via client e server, ele pode ser ambos, todavia, o seu código interno sempre será server-side, executado no server-side
		//mostrar APIs server side
		Tipos de Script Include:
			1 - Store One Classless Function
				guarda uma função reutilizavel
				é apenas usada server side
				também conhecida como on demand
			2 - Define a New Class
				coleção de funções
				pode ser chamada via client-side ou server-side
				padrão a ser incluso: "utils" no nome para representar utilidades
			3 - Extend an Existing Class
				adiciona funcionalidade a uma classe existente
				pode ser client-side ou server-side

Explicar a diferença de uma BR e de um script include, inclusive, fazer uma demo disso.


Store one classless/on demand
	nome dessa função deve ser o mesmo do Script Include
	mesmo que selecione o "client callable" ele não poderá rodar client=side

Define a New Class
	basicamente você guarda múltiplas funções
	depois do registro ser nomeado, um Script Editor Macro é inserido no campo de script
	o nome do SI deve ser igualzinho ao da classe.
	type é onde definimos o tipo da classe.
	//explicar o código rapidamente
	///////////////////////////////////////
	Outra forma é chamar uma reference qualifier Script Include. Esse é um tipo especial de Script Include que pode ser usado dentro da classe. Então, em vez de construir multiplas funções para |diferentes coisas, pode-se criar funções que só estão lá para filter registros em uma tabela alvo. Então, isso é o que um reference qualifier faz: ele filtra o que você programa.
	//////////////////////////////////////
	há o simples, para filtros estáticos.
	dinâmico, para rodar uma query dinâmica contra um campo de referencia.
	avançado, que permite definir o filtro diretamente no campo.
	Criar demo disso



Extend an Existing Class:
	-------------------------------------
	<img width="560" height="181" alt="Pasted image 20250811171541" src="https://github.com/user-attachments/assets/f4c0ed85-3b94-4de8-bb2d-c2e5115893aa" />
	use sempre o metodo extendsObject()
	estende uma classe para adicionar novas funcionalidades.
	--------------------
	Isso ocorre no AJAX processor Class, pois ela executa server-side, mas é chamada client-side
	Quando selecionamos Client Callable estamos fazendo isso,
	No Client Callable usamos o GlideAjax para o front.
	----------------
	O GlideAjax permite o Client Script e as UI Policies chamarem o server-side via Script include.
 	-------------------------------------
	<img width="652" height="321" alt="Pasted image 20250811173645" src="https://github.com/user-attachments/assets/62cdc8ca-2e7f-4d5c-bbed-f83433c97b2f" />
	<img width="610" height="386" alt="Pasted image 20250811175504" src="https://github.com/user-attachments/assets/fe940a57-a2d9-4c8d-8cd5-231b92499317" />



Uma boa prática é minimizar as consultar ao servidor (server lookups).



escopo de aplicação
	pode ser pública ou privada
	explicar o que é rapidamente
	há a protection policy:
		esse assegura que a propriedade é apenas leitura (não pode modificar) ou protegido, ou seja, no protegido sua lógica não é visualizável. O padrão (out of box) é o none.
		só funciona se o script include ou a aplicação que o contém esttá sendo instalado pelo SN application store ou pelo app repository.
	A sintaxe para chamar um Script Include depende do escopo.
	-------------------------------------
	<img width="618" height="233" alt="Pasted image 20250812140136" src="https://github.com/user-attachments/assets/9d692c19-e681-4390-aef4-e5f9478a0ac5" />
	<img width="645" height="323" alt="Pasted image 20250812140248" src="https://github.com/user-attachments/assets/2ec61db1-0be1-4e26-bec6-ec47eef0bd2a" />
	<img width="614" height="383" alt="Pasted image 20250812143845" src="https://github.com/user-attachments/assets/184d5a34-dae5-4cd4-8b9b-816209199315" />
	<img width="631" height="378" alt="Pasted image 20250812143941" src="https://github.com/user-attachments/assets/9db52192-dc3c-471d-a9f6-b01340cb8305" />


Por que usar?
	reusabilidade através da plataforma
	mantenabilidade
 
Quando usar?
	Sempre que tiver um pedaço de código que está sendo utilizado em dois lugares diferentes da SN. Se estou usando duas BRs que possuem o mesmo código, então eles basicamente fazem a mesma coisa, apenas com objetos diferentes, nisso se usa o script include
 
Como?
	É usada em quase toda aplicação, definir a função uma vez e depois chama-la.
