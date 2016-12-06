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
```
