# atividades-mongodb
Atividades banco mongoDB

```js
db.<nome-da-collection>.<operacao-desejada>
db.colecao1.count();
```

### Exemplo com resultados megasena
```js
db.megasena.count();
```

### Busca todos
```js
db.<colecionation>.find();
db.megasena.find();
```

### Busca apenas primeiro registro
```js
db.megasena.findOne();
```
### Parâmetros find
```js
db.<collection>.find(<campo1>)
db.megasena.find({"Concurso":73});
```

### Exibição resultados
```js
db.megasena.find({"Concurso":73}).pretty();
db.megasena.find({"Ganhadores_Sena":5});
```

Por padrão exibe todas as colunas. Para restringir alguns campos:

```js
db.<collection>.find({<campo1>:<valor>},{<campoParaExibir>:<exibeOuNaoExibe>});

db.megasena.find({"Ganhadores_Sena":5},{"Concurso":1});
db.megasena.find({"Ganhadores_Sena":5},{"Concurso":true,
					"_id":false});
db.megasena.find({"Ganhadores_Sena":5}, {"Concurso":1, "_id":0});
```

### Inserindo registros

```js
db.<collection>.insert({<campo>:<valor>});

db.megasena.insert(
{ 
 "Concurso" : 99999,
 "Data Sorteio" : "19/06/2014",
 "1 Dezena" : 1,
 "2 Dezena" : 2,
 "3 Dezena" : 3,
 "4 Dezena" : 4,
 "5 Dezena" : 5,
 "6 Dezena" : 6,
 "Arrecadacao_Total" : 0,
 "Ganhadores_Sena" : 0,
 "Rateio_Sena" : 0,
 "Ganhadores_Quina" : 1,
 "Rateio_Quina" : 88000,
 "Ganhadores_Quadra" : 55,
 "Rateio_Quadra" : 76200,
 "Acumulado" : "NAO",
 "Valor_Acumulado" : 0,
 "Estimativa_Prêmio" : 0,
 "Acumulado_Mega_da_Virada" : 0
});
```

Ex: ganhador

```js
db.ganhadores.count();

db.ganhadores.insert({"Concurso":99999,
		      "CPF":12345678909});

db.ganhadores.insert({"Concurso":99999,
		      "CPF":12345678909,
                      "Nome":"Coffin Joe"});

db.ganhadores.find().pretty();
```

### Atualizando registros

```js
db.<collection>.update(
{<criterioBusca>:<valor>},
{<campoAtualizar>:<novoValor>}
);

db.ganhadores.update(
{"_id":ObjectId("5846edb36cad189cb335c440")},
{"Nome": "Novo nome"});

db.<collection>.update(
{<criterioBusca>:<valor>},
{$set: {<campoAtualizar>:<novoValor>}});

db.ganhadores.update(
{"_id":ObjectId("5846edb36cad189cb335c440")},
{$set:{"NOme":"Nome alterado"}});
```

Por padrão altera apenas o primeiro registro encontrado. Para alterar todos os registros usa o multi.

```js
db.ganhadores.update({}, {$set:{"CPF":55555555555}});
```

Alterando multi para true, todas as linhas são alteradas.

```js
db.ganhadores.update({},
{$set:{"CPF":55555555555}},{multi:true});
```

### Upsert
Busca registro, se existir atualizar, senão cadastra.

```js
db.ganhadores.update({"Nome":"Mula sem cabeça"},
{$set:{"CPF":33333333333}},
{multi:0,upsert:0});

db.ganhadores.update({"Nome":"Mula sem cabeça"},
{$set:{"CPF":33333333333}},
{multi:0,upsert:1});
```

### Remover registros

```js
db.<collection>.remove({<criterioBusca>:<valor>});
```

Removendo todos os registros com CPF 33333333333:

```js
db.ganhadores.count();
db.ganhadores.find({"CPF":33333333333}).count();
db.ganhadores.remove({"CPF":33333333333});
db.ganhadores.count();
```
Para remover todos os registros de uma collection, é só passar uma condição vazia.

```js
db.ganhadores.count();
db.ganhadores.remove({});
db.ganhadores.count();
```

### Remover collections

```js
db.<collection>.drop();
```
