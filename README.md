## Bem vindo ao DapperBr

<p>Este site é para desenvolvedores que desejam aprender como usar o Dapper, o micro ORM desenvolvido pela equipe do StackOverflow.</p>
<p>Caso queira contribuir com essa documentação, fique a vontade em mandar um PR para nós! </p>

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
