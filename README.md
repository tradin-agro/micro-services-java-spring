# Micro Services com Java Spring

Micro services com Java Spring é um projeto fictício para teste das soluções Spring Clound.
Neste projeto foram implementadas a APIs de micro serviço, Migrations (para tratar de criação
e versionamento dos scripts de banco de dados MySQL), Service Discovery, Balanceamento de Carga,
API Gateway para centralização de requisições, Circuit Breaker e Fallback (resiliência a falhas).

### 🛠 Tecnologias
1. JDK 17
2. Maven 3
3. Spring Boot 3.2.2
4. MySQL
5. Eureka by Netflix
6. Flyway
7. Lombok
8. Model Mapper
9. OpenFeign
10. Resilience4J
11. Spring OAP

### ⚙️ Funcionalidades

- [x] Cadastro de pagamentos
- [x] Cadastro de pedidos
- [x] Integração síncrona de pagamentos com pedidos

### Instruções para uso da arquitetura

![alt text](arquitetura-spring-cloud-projeto-ms.png)

Os projetos estão organizados em submodulos para melhor entendimento. Faça o clone de todos
os projetos utilizando o comando:

```git clone --recursive https://github.com/tradin-agro/micro-services-java-spring.git```

- Abra cada um dos projetos individualmente na sua IDE, e execute o arquivo main de cada projeto
começando pelo projeto Eureka, depois Gateway, em seguida as aplicações.
- Para testar o balanceamento use endpoint de porta http://localhost:8082/pedidos-ms/pedidos/porta
- Antes do teste de balanceamento deverá subir uma nova instância da aplicação, informando 
o caminho do java da sua máquina mais o comando do jar instalado na pasta target do projeto Pedido.
Por exemplo: ```C:\Oracle\java\jdk-17\bin\java -jar pedidos-0.0.1-SNAPSHOT.jar br.com.tradin.pedidos.PedidosApplication```
no prompt do Windows (se for o seu caso), o comando funcionará na pasta /target. Conforme vai
subindo instâncias, as portas a cada requisição vão sendo alternadas.
- Para testar o Circuit Breaker e Fallback, deverá inserir um novo pagamento e um novo pedido. O 
pagamento inserido deve estar vinculado ao id do pedido. Derrube todas as instâncias do projeto
pedido e aguarde algum tempo. Depois execute o endpoint http://localhost:8082/pagamentos-ms/pagamentos/2/confirmar
informando na URL o id do seu pagamento. O pagamento será salvo com o status CONFIRMADO_SEM_INTEGRACAO, e o 
registro do pegido não terá seu status atualizado. Poderá testar também com pedido funcionando, onde
o status do pedido será atualizado, executando normalmente a integração.
- No endereço http://localhost:8081 vai acessar a página do Eureka server, onde poderá ver as
instâncias de aplicação que estão rodando naquele momento. 
- A instância Gateway está configurada para rodar no endereço http://localhost:8082 e as requisições
para os aplicativos registrados devem usar o nome de registro da aplicação, por exemplo: 
http://localhost:8082/pedidos-ms/pedidos e http://localhost:8082/pagamentos-ms/pagamentos
- Seu arquivo de properties de cada projeto deve ser configurado com o seu usuário e senha do 
banco de dados MySQL.

## 📝 Licença

Este repositório é livre, estude bastante e seja feliz!<br/>
Em caso de dúvidas, entre em contato<br/>
Giovanni Biffi<br/>
Tradin Ltda<br/>