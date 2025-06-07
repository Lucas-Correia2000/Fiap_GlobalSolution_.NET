# 🌍 GeoMonitor – Plataforma para Monitoramento e Resposta a Desastres  
**Desenvolvido no contexto do Global Solution - FIAP** 

> **Integrantes:**  
> Bruno Nogueira Burian - RM552863  
> Lucca Augusto Matteoni - RM98146  
> Luccas dos Anjos Correia da Silva - RM552890


## 🌪️ Visão Geral

Com o agravamento dos fenômenos climáticos e o aumento dos riscos ambientais, surge a necessidade de soluções tecnológicas que aliem monitoramento contínuo, análise preditiva e resposta ágil. O **GeoMonitor** surge como uma plataforma desenvolvida em **.NET 8**, integrando sensores IoT, inteligência artificial e mensageria, capaz de transformar dados em ações rápidas para proteger vidas e o meio ambiente.

## 🎯 Propósito do Projeto

- Supervisionar em tempo real áreas vulneráveis a desastres naturais.
- Permitir o registro e a categorização automática de eventos críticos.
- Gerar alertas dinâmicos baseados em informações sensoriais e descrições dos relatos.
- Facilitar a mobilização de equipes de resposta por meio de notificações automáticas.
- Disponibilizar consultas e relatórios através de uma API documentada e amigável.

## 👥 Público-Alvo

- **Comunidade e cidadãos:** podem relatar situações como enchentes, quedas de energia, árvores caídas, entre outros.
- **Órgãos públicos e Defesa Civil:** recebem informações em tempo real via RabbitMQ, otimizando a tomada de decisão.
- **Inteligência Artificial:** utiliza ML.NET para classificar automaticamente o tipo de ocorrência, agilizando o fluxo de triagem.

## 🏛️ Arquitetura e Componentes Principais

- **API desenvolvida em .NET 8:** expõe endpoints RESTful para integração e consultas.
- **RabbitMQ:** responsável pelo fluxo assíncrono de mensagens e processamento paralelo de eventos.
- **ML.NET:** modelo embarcado para classificação automatizada de ocorrências conforme a descrição.
- **Banco de Dados Oracle:** armazenamento robusto para usuários, eventos e tipos de ocorrência.
- **xUnit:** cobertura de testes para garantir qualidade e estabilidade da aplicação.

## 🚀 Funcionalidades-Chave

- Cadastro e gerenciamento de áreas de risco, usuários e tipos de ocorrências.
- Registro de eventos com previsão automática do tipo via IA.
- Envio de notificações assíncronas para equipes de resposta utilizando RabbitMQ.
- Endpoints documentados e acessíveis pelo Swagger UI.
- Testes automatizados para todas as principais regras de negócio.

## 🔨 Tecnologias e Ferramentas

- .NET 8
- Oracle.EntityFrameworkCore
- RabbitMQ.Client
- ML.NET
- Swagger (OpenAPI)
- xUnit
- AspNetCoreRateLimit

## 📁 Estrutura do Projeto

```
GeoMonitor.API/
 ├── Controllers/
 │    ├── OcorrenciaController.cs
 │    ├── UsuarioController.cs
 │    └── TipoOcorrenciaController.cs
 ├── DTOs/
 ├── Models/
 ├── Services/
 │    ├── RabbitMQService.cs
 │    └── MLModelService.cs
 ├── Data/
 │    └── AppDbContext.cs
 └── Program.cs

GeoMonitor.Tests/
 ├── UsuarioControllerTests.cs
 ├── OcorrenciaTests.cs
 └── TipoOcorrenciaTests.cs

GeoMonitor.Consumer/
 └── Program.cs
```

## ⚙️ Como Executar

### Pré-requisitos
- .NET 8 SDK
- Oracle Database (local ou hospedado)
- RabbitMQ (pode ser executado via Docker)
- Visual Studio 2022+ ou VS Code

### Passos Básicos

1. Configure a string de conexão no `appsettings.json`:
    ```json
    "ConnectionStrings": {
      "OracleConnection": "Data Source=oracle.fiap.com.br:1521/orcl;User Id=SEU_USUARIO;Password=SUA_SENHA;"
    }
    ```
2. Compile e execute a API:
    ```
    dotnet build
    dotnet run --project GeoMonitor.API
    ```
3. Inicie o consumidor RabbitMQ:
    ```
    dotnet run --project GeoMonitor.Consumer
    ```
4. Execute os testes automatizados:
    ```
    dotnet test
    ```
## 📬 Integração com RabbitMQ

- **Envio:** Ao registrar um novo evento (POST /api/Ocorrencia), os dados são publicados na fila `fila_ocorrencias`.
- **Consumo:** O módulo GeoMonitor.Consumer escuta a fila e processa as mensagens, podendo evoluir para geração de alertas, dashboards ou logs.

## 🤖 Inteligência Artificial (ML.NET)

O endpoint de previsão permite identificar o tipo de ocorrência a partir da descrição, facilitando a triagem e resposta:

```
POST /api/Ocorrencia/prever
{
  "descricao": "Bairro sem energia após forte chuva"
}
```
Resposta esperada:
```json
{ "tipoPrevisto": "Falta de energia" }
```

## ✅ Testes Automatizados

Inclui cenários para criação de usuários, inserção e classificação de ocorrências, cadastro de tipos e integração RabbitMQ, garantindo robustez e confiabilidade.

## 🌱 Impacto Esperado

Ao unir sensores, IA e processamento assíncrono em um ambiente .NET moderno, o GeoMonitor contribui para cidades mais inteligentes, resilientes e seguras, promovendo a tomada de decisões rápidas e embasadas em situações de emergência.

---
