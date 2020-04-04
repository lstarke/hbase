#### 1. Crie a tabela com 2 famílias de colunas:

a. personal-data
b. professional-data

```
create 'italians', 'personal-data', 'professional-data'
```

#### 2. Importe o arquivo via linha de comando
```
hbase shell italians
```
#### Agora execute as seguintes operações:
#### 1. Adicione mais 2 italianos mantendo adicionando informações como data de nascimento nas informações pessoais e um atributo de anos de experiência nas informações profissionais;

```
put 'italians', '11', 'personal-data:name', 'Leandro Starke'
put 'italians', '11', 'personal-data:bithday', '1984-01-05'
put 'italians', '11', 'professional-data:role', 'Analista CAD'
put 'italians', '11', 'professional-data:salary', '5000'
put 'italians', '11', 'professional-data:experience', '3'
put 'italians', '12', 'personal-data:name', 'Jéssica Knopf'
put 'italians', '12', 'personal-data:bithday', '1991-04-06'
put 'italians', '12', 'professional-data:role', 'Empresária'
put 'italians', '12', 'professional-data:salary', '6000'
put 'italians', '12', 'professional-data:experience', '7'
```
#### 2. Adicione o controle de 5 versões na tabela de dados pessoais.

```
alter 'italians', {NAME=>'personal-data', VERSIONS=>5}
```
#### 3. Faça 5 alterações em um dos italianos;

```
put 'italians', '11', 'personal-data:name', 'Starke'
put 'italians', '11', 'personal-data:bithday', '1983-01-05'
put 'italians', '11', 'professional-data:role', 'Analista CAD Senior'
put 'italians', '11', 'professional-data:salary', '8000'
put 'italians', '11', 'professional-data:experience', '8'
```
#### 4. Com o operador get, verifique como o HBase armazenou o histórico.

```
scan 'italians', {VERSIONS=>5}
```

#### 5. Utilize o scan para mostrar apenas o nome e profissão dos italianos.

```
scan 'italians', {COLUMNS=>['personal-data:name','professional-data:role']}
```

#### 6. Apague os italianos com row id ímpar

```
deleteall 'italians', '1'
```

#### 7. Crie um contador de idade 55 para o italiano de row id 5

```
incr 'italians', '5', 'personal-data:age', 55
```

#### 8. Incremente a idade do italiano em 1

```
incr 'italians', '5', 'personal-data:age', 1
```
