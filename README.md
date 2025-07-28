# Microsserviço de Envio de E-mails

## Visão Geral
O **Microsserviço de Envio de E-mails** é um microsserviço baseado em Java projetado para gerenciar o envio de e-mails em uma arquitetura de microsserviços. Ele utiliza o Spring Boot para construir a aplicação e se integra ao RabbitMQ para processamento assíncrono de mensagens, garantindo um envio de e-mails confiável e escalável.

## Funcionalidades
- **Envio Assíncrono de E-mails**: Processa solicitações de e-mails de forma assíncrona usando filas do RabbitMQ.
- **Arquitetura Escalável**: Construído como um microsserviço, permitindo implantação independente e escalabilidade conforme necessário.
- **Configurável**: Facilmente configurável para diferentes provedores de e-mail e configurações.
- **Tratamento Robusto de Erros**: Garante entrega confiável de e-mails com mecanismos de retentativa e registro de erros.

## Tecnologias Utilizadas
- **Java**: Linguagem principal de programação do microsserviço.
- **Spring Boot**: Framework para construção da aplicação, fornecendo injeção de dependências, configuração e APIs RESTful.
- **Spring AMQP**: Para integração com o RabbitMQ, gerenciando publicação e consumo de mensagens.
- **RabbitMQ**: Corretor de mensagens para comunicação assíncrona, garantindo processamento de e-mails desacoplado e confiável.
- **Maven**: Ferramenta de gerenciamento de dependências e construção.

## Primeiros Passos

### Pré-requisitos
- Java 17 ou superior
- Maven 3.6+
- Servidor RabbitMQ (local ou remoto)
- Uma conta em um provedor de serviços de e-mail (por exemplo, credenciais SMTP para Gmail, SendGrid, etc.)

### Instalação
1. **Clonar o repositório**:
   ```bash
   git clone https://github.com/viktormendes/send-email-microservice.git
   cd send-email-microservice
   ```

2. **Configurar o RabbitMQ**:
   - Certifique-se de que um servidor RabbitMQ está em execução.
   - Atualize o arquivo `application.properties` ou `application.yml` com os detalhes da conexão ao RabbitMQ:
     ```properties
     spring.rabbitmq.host=localhost
     spring.rabbitmq.port=5672
     spring.rabbitmq.username=guest
     spring.rabbitmq.password=guest
     ```

3. **Configurar as Definições de E-mail**:
   - Atualize as configurações do provedor de e-mail em `application.properties` ou `application.yml`:
     ```properties
     spring.mail.host=smtp.example.com
     spring.mail.port=587
     spring.mail.username=seu-email@example.com
     spring.mail.password=sua-senha
     spring.mail.properties.mail.smtp.auth=true
     spring.mail.properties.mail.smtp.starttls.enable=true
     ```

4. **Construir o projeto**:
   ```bash
   mvn clean install
   ```

5. **Executar a aplicação**:
   ```bash
   mvn spring-boot:run
   ```

### Uso
- **Enviar um E-mail**:
  - O microsserviço escuta mensagens em uma fila do RabbitMQ (por exemplo, `email.queue`).
  - Publique uma mensagem na fila com os detalhes do e-mail (por exemplo, destinatário, assunto, corpo) em formato JSON:
    ```json
    {
      "to": "destinatario@example.com",
      "subject": "E-mail de Teste",
      "body": "Este é um e-mail de teste enviado pelo microsserviço."
    }
    ```
  - O microsserviço processará a mensagem e enviará o e-mail por meio do provedor configurado.

### Exemplo
Para enviar uma mensagem à fila do RabbitMQ, você pode usar um endpoint REST (se implementado) ou um cliente RabbitMQ. Exemplo usando `curl` com uma API REST (se disponível):
```bash
curl -X POST http://localhost:8080/api/email/send \
-H "Content-Type: application/json" \
-d '{"to":"destinatario@example.com","subject":"E-mail de Teste","body":"Olá do Microsserviço de Envio de E-mails!"}'
```

## Contribuição
Contribuições são bem-vindas! Por favor, faça um fork do repositório e envie um pull request com suas alterações.

1. Faça um fork do repositório.
2. Crie uma nova branch (`git checkout -b feature/sua-funcionalidade`).
3. Faça commit das suas alterações (`git commit -m "Adiciona sua funcionalidade"`).
4. Envie para a branch (`git push origin feature/sua-funcionalidade`).
5. Abra um pull request.

## Licença
Este projeto está licenciado sob a Licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

## Contato
Para perguntas ou feedback, entre em contato com [viktormendes](https://github.com/viktormendes).
