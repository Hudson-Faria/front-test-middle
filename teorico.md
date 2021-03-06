# Teórico

1\) Qual a diferença do operador `==` para o operador `===` em JavaScript?

== Realiza comparação apenas de valor    				<br />
=== Realiza comparação de valor e tipo

1.1) Dê 2 exemplos de quando os operadores produziriam resultados diferentes

 var numero = 1; // Variavel responsavel por realizar as condições 	<br />
 // Primeiro exemplo utilizando o operador (==) 			<br />
 if (numero == '1') 							<br />
 { <br />
    alert("Igual");		 					<br />
 } 									<br />
 else 									<br />
 { <br />
    alert("Diferente"); 						<br /> 
 } <br />
 // Primeiro exemplo utilizando o operador (===) 			<br />
 if (numero === '1') 							<br />
{ <br />
	alert("Igual"); 						<br />
} 									<br />
else 									<br /> 
{ 									<br />
    alert("Diferente"); 						<br />
} 									<br />

Nesse primeiro exemplo com o operador == o resultado será exibido como igual e utilizando o operador === o resultado será exibido como diferente.

// Segundo exemplo utilizando o operador (==)				<br />
alert("123 milhas" == new String("123 milhas"));			<br />

// Segundo exemplo utilizando o operador (===)				<br />
alert("123 milhas" === new String("123 milhas"));

Nesse segundo exemplo com o operador == retornará true e com o operador === retornará false

2\) Recursos/Práticas:

2.1) Qual recurso do javascript é mais recomendado para tratar processamentos asíncronos? Justifique.

Async

O módulo async é uma lib usada para gerenciar o fluxo assíncrono de operações em Javascript. Com este módulo, podemos controlar a ordem de execução das operações. A proposta das funções async/await é de simplificar o uso de forma síncrona das Promises e executar alguns procedimentos em um grupo de Promises. Assim como Promises são similares a callbacks estruturados, funções async/await são similares à junção de generators com Promises.

2.2) Quais os recursos mais recomendados para incluir ícones em um site? Justifique.

Favicon

Um favicon (abreviação de ícone favorito), também conhecido como ícone de atalho, ícone de site, ícone de guia, ícone de URL ou ícone de favoritos, é um ou mais pequenos ícones associados a um site ou uma página web específica.


2.3) Qual recurso dos browsers é usado para carregar dados/conteúdos dinâmicos sem recarregar a página? Existem alternativas?

Ajax. Existe outra possibilidade utilizando iframe.

2.4) Qual recurso angular pode ser usado para aumentar a performance de campos que realizam algum processamento ao alterar o texto?

Watchers.

2.5) Por quê é importante diminuir a quantidade de watchers do angular em uma página e como fazer?

Para evitar uma quantidade de loops e requisiçõe ajax do javascript evitando executar uma lista de $watches. Oque poderá acarretar em uma maior lentidão da página. Utilizando a anotação :: para permitir expressões constantes e evitar o disparo de watchers desnecessários. 

2.6) Por quê é importante evitar escopos isolados em diretivas do angular e como fazer?

Em determinados momentos não permite uma expansão do elemento isolado, fazendo com que a mudança interfira em todo conteúdo. Temos que pensar em algo como uma propriedade. Uma solução seria o templateUrl. Quando as diretivas começam a se tornar mais complexas, o template deixa de oferecer um organização sustentável, então outra solução seria mover uma página só para ele. 

---

3\) CSS:

3.1) Por quê é importante não fazer seletores por tags html?

Pois não permite uma estilização de um conjunto maior das tags especificas. Por exemplo estilizando uma tag p do html todos as outras tag p criadas terão o mesmo estilo. Criando classes ou identificadores permite um estilo individual para cada tag.

3.2) Para criar um site que desse a opção do usuário escolher um tema, qual tecnogia/recurso de css você utilizaria?

Gosto de utilizar o Wordpress (CMS para conteúdo) e o Framework Bootrstrap. Nesse caso eu utilizaria algum template do bootstrap ou do Wordpress. Uma observação é que alguns templates do wordpress implementam o bootstrap. 

3.3) Quais práticas/recursos devem ser usados para criar sites responsivo?

No código seria o uso de um recurso do css chamado @medias, que nós permite estilizar para direfentes tamanhos de telas. Alguns frameworks desenvolvidos usados no mercado já implementam esses recuros, facilitando esse trabalho. Sendo um dos mais utilizados o bootstrap, particularmente oque eu mais gosto de usar. No desenvovimento seria mobile-first que é o desenvolvimento inicial do layout primeiramente para dispositivos mobiles e depois adaptando para outros dispositivos, favorecer sempre a velocidade do site, eliminar oque não é essencial, criar botões que convertam e sempre fazer testes de usabilidade. 

3.4) Quais metodologias CSS você costuma seguir? Explique um pouco delas.

O uso de arquivos separados de estilos, boa modulariação de classes uso de pré-processadores e alguns frameworks. 

Arquivos separdos nós permite uma maior legibilidade e uma mais fácil manutenção, modulariando classes em arquivos separados para um arquivo ou conjuntos de tags especificas e utilizando frameworks como Less e Sass nós permite criar códigos css dinâmicos e com design patterns melhores escritos. 

---

4\) Análise de código

4.1) Quanto tempo vai demorar para o código a seguir imprimir "finished"? Justifique. (Levando em consideração que `somePromise()` vai retornar uma Promise resolvida)
```js
function doSomething() {
    return new Promise(resolve => {
        setTimeout(resolve, 1000)
    })
}

function doSomethingElse() {
    return new Promise(resolve => {
        setTimeout(resolve, 2000)
    })
}

somePromise()
    .then(() => {
        doSomething()
        doSomethingElse()
    })
    .then(() => {
        console.log('finished')
    })

```

3 Segundos.

doSomething() executara depois de 1 segundo, após doSomethingElse() executara depois de 2 segundos, somePromise() executara essa que resultará em 3 segundos.  Uma observação, a função Promise.race recebe uma lista de promises e assim que uma delas for resolvida, receberemos imediatamente seu resultado na próxima chamada encadeada à then. Se esse recurso estivesse implementado o resultado seria apenas 1 segundo.   

4.2) O que o código a seguir imprime? (Levando em consideração que `somePromise()` vai retornar uma Promise resolvida)
```js
somePromise()
    .then(() => {
        throw new Error('uh oh!')
    }, err => {
        console.log(err.message)
    })
    .then(() => {
        console.log('ok now!')
    })
```

ok now!
A exceção lançada em throw não será lançada pois o segundo .then() executara sem erros.



4.3\) Quais as vantagens/desvantagens da segunda função em relação a primeira?
```js
function doSomething(options) {
    return fetch(options.url).then(r => r.json())
}

async function doSomethingAsync(options) {
    return fetch(options.url).then(r => r.json())
}
```

Implementado como um método assincrono. O recomendado no uso do assincronimos são em operações que tem o tempo de execução no minimo em 50 milisegundos, menos do que esse isso não é compensatorio.Na verdade em determinadas ações o melhor é não usar, não é utilizado para tornar algo mais rápido ou melhorar performance, o ganho de métodos assíncronos são execuções em paralelo podendo atender mais requisições. 


5\) Quais as vantagens de usar ES modules em vez de usar commonjs?

Os módulos oferecem uma maneira melhor de organizar variaveis e funções. Com os módulos, você agrupa as variáveis e funções podendo ser incluidas juntas, fornecendo também uma evolução no controle de dependencias com o parser de módulos totalmente separado dos scripts, sempre carregados assincronamente e Exports nomeados.

6\) Cite as principais diferenças entre um componente e uma diretiva no AngularJS.

Diretivas são usadas como extensão do HTML (como tags ou atributos) para manipulação do DOM, contém alguns problemas com data-binding e escopos. O componente vem como as proposta para solução destes problemas das diretivas, isolando escopos, lidando melhor com o data-binding, manipulação mais avançada do DOM, e também para começar adaptar o código mais próximo dos moldes do Angular.
