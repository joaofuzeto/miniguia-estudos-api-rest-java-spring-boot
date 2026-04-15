# miniguia-estudos-api-rest-java-spring-boot
Criando um repositório para documentar os estudos em criação de API REST com Java e Spring Boot

# 🚀 Contexto e Objetivo

Estudar construção de APIs REST com Spring Boot, com foco em boas práticas e arquitetura backend.

# 📚 Fontes Utilizadas
Spring Boot Docs <https://docs.spring.io/spring-boot/docs/0.0.x/reference/htmlsingle/?utm_source=chatgpt.com>
Baeldung <https://www.baeldung.com/spring-tutorial?utm_source=chatgpt.com>
Oracle Java Docs <https://docs.spring.io/spring-boot/index.html?utm_source=chatgpt.com>
Dev.to <https://dev.to/zuplo/spring-boot-api-tutorial-build-document-and-secure-a-rest-api-3mn9>

# 🤖 Engenharia de Prompts
**Prompt 1:**
```
Explique como funciona o ciclo de vida de uma aplicação Spring Boot, com foco em criação de APIs REST
```

**Resposta:**
```
O ciclo de vida de uma aplicação Spring Boot, especialmente voltada para a criação de APIs REST, é projetado para ser automatizado e eficiente, permitindo que desenvolvedores criem aplicações "prontas para produção" com configuração mínima
.
Abaixo, detalho as etapas fundamentais desse ciclo de vida com base nas fontes:
1. Inicialização e Bootstrap
Tudo começa com o método main, que atua como o ponto de entrada da aplicação Java
. Dentro dele, a execução é delegada à classe SpringApplication.run(), que realiza o bootstrap da aplicação
.
Detecção de Ambiente: O Spring Boot tenta determinar se a aplicação é web ou não. Para uma API REST, ele detecta a presença de classes web no classpath e inicia um AnnotationConfigEmbeddedWebApplicationContext
.
Eventos Iniciais: Durante a inicialização, são disparados eventos como o ApplicationStartedEvent (no início da execução) e o ApplicationEnvironmentPreparedEvent (quando o ambiente de configuração já é conhecido, mas o contexto ainda não foi criado)
.
2. Configuração Externa e Preparação do Ambiente
O Spring Boot carrega configurações de diversas fontes de forma hierárquica para permitir que o mesmo código funcione em diferentes ambientes
.
Prioridade de Propriedades: Ele busca configurações em argumentos de linha de comando, variáveis de ambiente do sistema operacional e arquivos como o application.properties ou application.yml
.
Perfis (Profiles): É possível segregar partes da configuração para ambientes específicos (como dev ou prod) usando spring.profiles.active
.
3. Auto-configuração e Registro de Beans
Esta é a fase onde a "mágica" do Spring Boot acontece através da anotação @EnableAutoConfiguration (geralmente incluída na @SpringBootApplication)
.
Opinião sobre o Classpath: O Spring Boot "adivinha" quais configurações você precisa com base nas dependências adicionadas
. Por exemplo, ao incluir o spring-boot-starter-web, ele configura automaticamente o Tomcat embutido e o Spring MVC
.
Escaneamento de Componentes: Através do @ComponentScan, o Spring localiza e registra classes anotadas com @RestController, @Service e @Repository como Beans gerenciados no contexto
.
4. Ciclo de Vida em Execução (API REST)
Uma vez que o contexto está pronto, a API REST entra em operação:
Servidor Embutido: O Spring Boot inicia o servidor (ex: Tomcat ou Jetty) na porta configurada (padrão 8080)
.
Roteamento de Requisições: O DispatcherServlet recebe as requisições HTTP e as mapeia para os métodos apropriados dentro dos seus @RestController usando informações de roteamento da anotação @RequestMapping
.
Conversão de Mensagens: Para APIs REST, o Spring utiliza HttpMessageConverters (como a biblioteca Jackson) para converter automaticamente objetos Java em JSON nas respostas e vice-versa nas requisições
.
5. Monitoramento e Gerenciamento (Actuator)
Em produção, o ciclo de vida inclui o monitoramento contínuo. Ao adicionar o Spring Boot Actuator, a aplicação expõe endpoints como /health (saúde) e /metrics (métricas) para que ferramentas externas possam gerenciar a instância
.
6. Encerramento (Shutdown)
O Spring Boot registra um shutdown hook na JVM para garantir que o ApplicationContext seja fechado de forma graciosa ao sair
.
Callbacks: Durante o encerramento, callbacks padrão como @PreDestroy ou a implementação da interface DisposableBean são executados para liberar recursos adequadamente
```

**Problema encontrado:**
```
A IA respondia de forma genérica.
```

**Tentativa:**
```
Refinei o prompt pedindo exemplos práticos.
```

**Resultado:**
```
Respostas mais aplicáveis ao contexto de backend Java.
```

# 📖 Miniguia de Estudo
## 📌 Resumo
O ciclo de vida de uma aplicação Spring Boot para APIs REST pode ser dividido em etapas bem definidas:

1. Inicialização (Bootstrap)
* A execução começa no método main()
* O SpringApplication.run() inicia o contexto da aplicação
* O framework detecta automaticamente se é uma aplicação web

👉 Resultado: o ambiente base da aplicação é preparado

2. Configuração do Ambiente
* Carregamento de configurações (application.properties ou .yml)
* Leitura de variáveis de ambiente
* Definição de perfis (dev, prod, etc.)

👉 Resultado: a aplicação se adapta ao ambiente sem mudar código

3. Auto-configuração
* Ativada por @SpringBootApplication
* O Spring configura automaticamente componentes com base nas dependências

Exemplo:

Adicionou spring-boot-starter-web → já vem com servidor embutido

👉 Resultado: menos código manual, mais produtividade

4. Registro de Beans
O @ComponentScan identifica:
* @RestController
* @Service
* @Repository

👉 Resultado: tudo passa a ser gerenciado pelo container do Spring

5. Execução da API REST
* Servidor (Tomcat) sobe automaticamente
* O DispatcherServlet intercepta requisições HTTP
* Endpoints são mapeados com @RequestMapping

Fluxo real:
```
Cliente → Controller → Service → Repository → Banco → Resposta JSON
```

👉 Resultado: API funcional respondendo requisições

6. Conversão de Dados
* Objetos Java ⇄ JSON automaticamente
* Feito via HttpMessageConverters (ex: Jackson)

👉 Resultado: comunicação padronizada via REST

7. Monitoramento (Actuator)
Endpoints como:
* /health
* /metrics

👉 Resultado: observabilidade da aplicação em produção

🔹 8. Encerramento
* Shutdown controlado via JVM

Execução de:
* @PreDestroy
* DisposableBean

👉 Resultado: liberação correta de recursos


## 📚 Glossário
* Spring Boot → Framework para criar aplicações Java rapidamente
* Bean → Objeto gerenciado pelo Spring
* ApplicationContext → Container que gerencia os Beans
* @RestController → Define endpoints REST
* DispatcherServlet → Controlador central das requisições HTTP
* Auto-configuração → Configuração automática baseada em dependências
* Profile → Configuração específica por ambiente
* Actuator → Ferramenta de monitoramento

## 🔁 Prompts reutilizáveis

**Para revisão de conceito**
```
Explique o ciclo de vida de uma aplicação Spring Boot com foco em APIs REST e dê exemplos práticos
```

**Para aprofundamento técnico**
```
Descreva o fluxo de uma requisição HTTP dentro do Spring Boot, desde o Controller até o banco de dados
```

**Para comparação**
```
Compare Spring Boot com Spring tradicional no contexto de criação de APIs REST
```

**Para prática**
```
Gere um exemplo de API REST em Spring Boot com Controller, Service e Repository
```

**Para debugging (nível mais avançado)**
```
Quais são os pontos mais comuns de falha no ciclo de vida de uma aplicação Spring Boot e como diagnosticar?
```
