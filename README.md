## Bem vindo ao DapperBr

<p>Este site é para desenvolvedores que desejam aprender como usar o Dapper, o micro ORM desenvolvido pela equipe do StackOverflow.</p>
<p>Caso queira contribuir com essa documentação, fique a vontade em mandar um PR <a href ="https://github.com/dapperbr/dapperbr.github.io">DapperBr</a></p>

### O que é Dapper?
<p>O Dapper é um micro ORM voltado para desenvolvedores .NET, onde seu principal objetivo é realizar o mapeamento de consultas em banco de dados para objetos.</p>

### O que é um micro ORM?
<p>Um micro ORM possuí apenas a funcionalidade de realizar mapeamento de consultas em objetos, diferentemente de um ORM como Entity Framework ou NHibernate que possui além do mapeamento de consultas em objetos várias outras características.</p> 
<p>Veja abaixo, as principais características de um ORM comparado com um micro ORM:</p>

|                                 | Micro ORM| ORM|  
| --------------------------------|:---: |:---: |
|  Mapeamento de Query em objetos |:+1:|:+1:|
|  Cache em resultados |:-1:|:+1:|
|  Tracking de Mudanças|:-1:|:+1:|
|  Geração de SQL	|:-1: ¹ |:+1:|
|  Gerenciamento de Identidade	|:-1:|:+1:|
|  Gerenciamento de Associação	|:-1:|:+1:|
|  Lazy Loading	|:-1:|:+1:|
|  Padrão Unit of Work | :-1:|:+1:|
|  Migração de Dados (Migrations) |:-1:|:+1:|

*1. O pacote Dapper.Contrib consegue fazer a geração de SQL, porém, somente para cenários simples.

### Quando usar o Dapper?
O Dapper foi desenvolvido para resolver problemas de performance em consultas SQL, portanto, caso seja o seu cenário de garantir performance e controle nas consultas SQl, Dapper pode ser uma boa solução comparado aos Orms, porém, cabe algumas ressalvas importantes antes de tomar essa decisão:

- *Testes automatizados são mais dificeis de serem realizados.*
- *O time tem que dominar SQL e ter controle sobre as consultas realizadas.

Em resumo, o Dapper é muito simples e facil de usar, e com compatibilidade com várias tipos de banco de dados, devido ao fato de ser implementado em cima do **IDbConnection** do **ADO.NET**.

### Como instalar o Dapper na minha aplicação?
Dapper está disponível nos pacotes Nuget, compatível com as aplicações Full Framework e .NET core.

Para a instalação a última versão via linha de comando, basta digitar o seguinte comando:

``` dotnet add package Dapper```

Para instalar a última versão no Package Manager Console no Visual Studio, basta digitar o seguinte comando:

``` install-package Dapper ```
 
O código fonte do Dapper está <a href="https://github.com/StackExchange/Dapper">disponível no GitHub</a>.
