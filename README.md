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
O Dapper foi desenvolvido para resolver problemas de performance em consultas SQL, portanto, caso seja este seu cenário de performance e controle em consultas SQL, Dapper pode ser uma boa solução comparado aos Orms, porém, cabe algumas ressalvas importantes antes de tomar essa decisão:

- *Testes automatizados são mais dificeis de serem realizados.*
- *O time tem que dominar SQL e ter controle sobre as consultas realizadas.*

Uma das qualidades do Dapper é sua implementação simples com poucas linhas você consegue realizar consultas e transações em banco de dados. Compatível com vários banco de dados, devido ao fato de utilizar várias implantações de ExtensionMethods na interface **IDbConnection** do **ADO.NET**.
### ADO.NET e o Dapper

Para realizar uma consulta em uma tabela de Pessoas, e mapear em um objeto você teria que realizar a seguinte implementação:

*A implementação com ADO.NET:*
```csharp
var sql = "select * from pessoas";
var pessoas = new List<Pessoa>();
using var conexao  = new SqlConnection(connString);

conexao.Open();
    
using var comando = new SqlCommand(sql, conexao);
using var leitor = commando.ExecuteReader();
        
            var pessoa = new Pessoa
            {
                PessoaId = leitor.GetInt32(leitor.GetOrdinal("PessoaId")),
                Nome = leitor.GetString(leitor.GetOrdinal("Nome")),
                Idade = leitor.GetInt32(leitor.GetOrdinal("Idade")),
                Email=  leitor.GetString(leitor.GetOrdinal("Email"))
            };
            pessoas.Add(pessoa);
```
*Agora, a implementação com Dapper:*
```csharp

var sql = "select * from pessoas";
var pessoas = new List<Pessoa>();
using var conexao  = new SqlConnection(connString);
pessoas = conexao.Query<Pessoa>(sql);
```

Como podemos perceber a implementação utilizando Dapper simplifica tratando das questões de mapeamento e commands para nós, economizando um bom tempo que gastaríamos implementando tudo isto na mão, e tornando a legibilidade do código simples.

### Como instalar o Dapper na minha aplicação?
Dapper está disponível nos pacotes Nuget, compatível com as aplicações Full Framework e .NET core.

Para a instalação a última versão via linha de comando, basta digitar o seguinte comando:

``` dotnet add package Dapper```

Para instalar a última versão no Package Manager Console no Visual Studio, basta digitar o seguinte comando:

``` install-package Dapper ```
 
O código fonte do Dapper está <a href="https://github.com/StackExchange/Dapper">disponível no GitHub</a>.

## Retornando multiplos registros ##
Existem alguns métodos que você pode usar para retonar multiplos registros, segue abaixo uma lista de métodos disponíveis no Dapper:
| Método | Descrição |
|--------|-----------|
|Query|Retorna um IEnumerable&lt;dynamic&gt; |
|Query<T>| Retorna um IEnumerable&lt;T&gt; |
|QueryAsync| Retorna um IEnumerable&lt;dynamic&gt; de forma assincrona|
|QueryAsync<T>| Retorna um IEnumerable&lt;T&gt; de forma assincrona|
    
A principal diferença está relacionada a tipagem. O método **Query** retorna um **IEnumerable** do tipo **dynamic** e o método genérico **Query&lt;T&gt;** retorna um **IEnumerable** de uma classe genérica **T**.

*Classe de Pessoas:*

```csharp
public class Pessoa
{
    public Guid Id{get;set;}
    public string Nome{get;set;}
    public int Idade{get;set;}
    public string Email{get;set;}
}
```
*Veja um exemplo abaixo, usando Query&lt;T&gt;:*

```csharp
var sql = "SELECT Id, Nome, Idade, Email FROM Pessoas";
using var conexao  = new SqlConnection(connString);
var pessoas = conexao.Query<Pessoa>(sql);
foreach(var pessoa in pessoas)
{
    Console.WriteLine(pessoa.Id);
    Console.WriteLine(pessoa.Nome);
    Console.WriteLine(pessoa.Idade);
    Console.WriteLine(pessoa.Email);
}
Console.ReadLine();
```
*Veja um exemplo abaixo, usando Query&lt;dynamic&gt;:*

```csharp
var sql = "SELECT Id, Nome, Idade, Email FROM Pessoas";
using var conexao  = new SqlConnection(connString);
var pessoas = conexao.Query(sql);
foreach(var pessoa in pessoas)
{
    Console.WriteLine(pessoa.Id);
    Console.WriteLine(pessoa.Nome);
    Console.WriteLine(pessoa.Idade);
    Console.WriteLine(pessoa.Email);
}
Console.ReadLine();
```
*Veja um exemplo abaixo, usando QueryAsync&lt;T&gt;:*


```csharp
var sql = "SELECT Id, Nome, Idade, Email FROM Pessoas";
using var conexao  = new SqlConnection(connString);
var pessoas = await conexao.QueryAsync<Pessoa>(sql);
foreach(var pessoa in pessoas)
{
    Console.WriteLine(pessoa.Id);
    Console.WriteLine(pessoa.Nome);
    Console.WriteLine(pessoa.Idade);
    Console.WriteLine(pessoa.Email);
}
Console.ReadLine();
```
*Veja um exemplo abaixo, usando QueryAsync&lt;dynamic&gt;:*

```csharp
var sql = "SELECT Id, Nome, Idade, Email FROM Pessoas";
using var conexao  = new SqlConnection(connString);
var pessoas = await conexao.QueryAsync(sql);
foreach(var pessoa in pessoas)
{
    Console.WriteLine(pessoa.Id);
    Console.WriteLine(pessoa.Nome);
    Console.WriteLine(pessoa.Idade);
    Console.WriteLine(pessoa.Email);
}
Console.ReadLine();
```
***Atenção:** O uso do dynamic pode trazer sérios problemas, pois,qualquer erro de escrita só será identificado em Runtime, por exemplo: Caso você informe ao invés o campos pessoa.Id, você informe pessoa.ID, o intellisense não irá reclamar, e ao executar o programa você irá ser surpreendido com um erro.*

## Retornando apenas um registro ##
Existem alguns métodos que você pode usar para retonar apenas um registros, segue abaixo uma lista de métodos disponíveis no Dapper:
| Método | Descrição |Exceções|
|--------|-----------|--------|
|QuerySingle|Retorna apenas um registro utilizando do tipo **dynamic** |Caso não retorne ou retorne mais de 1 registro, será lançada a exception InvalidOperationException.| 
|QuerySingle&lt;T&gt;| Retorna apenas um registro do tipo **T** |Caso não retorne ou retorne mais de 1 registro, será lançada a exception InvalidOperationException.|
|QuerySingleOrDefault| Retorna apenas um registro utilizando do tipo **dynamic**|Caso retorne mais de 1 registro, será lançada a exception InvalidOperationException.|
|QuerySingleOrDefault&lt;T&gt;| Retorna apenas um registro utilizando do tipo **T**|Caso retorne mais de 1 registro,será lançada a exception InvalidOperationException.|
|QueryFirst| Retorna apenas um registro utilizando do tipo **dynamic**|Caso não retorne registro, será lançada a exception InvalidOperationException.|
|QueryFirst&lt;T&gt;| Retorna apenas um registro utilizando do tipo **T**|Caso não retorne registro, será lançada a exception InvalidOperationException.|
|QueryFirst| Retorna apenas o primeiro registro utilizando do tipo **dynamic**|Caso não retorne registro, será lançada a exception InvalidOperationException.|
|QueryFirst&lt;T&gt;| Retorna apenas primeiro registro utilizando do tipo **T**|Caso não retorne registro, será lançada a exception InvalidOperationException.|   
|QueryFirstOrDefault| Retorna apenas primeiro registro ou null caso não exista registros, utiliza o tipo **dynamic**||
|QueryFirstOrDefault&lt;T&gt;| Retorna apenas primeiro registro ou null caso não exista registros, utiliza o tipo **T**|| 
