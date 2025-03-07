# TrackerHub Platform 🚀

Esta é uma aplicação base construída com Laravel, projetada para servir como ponto de partida para o projeto Platform. Ela inclui uma configuração inicial e algumas funcionalidades básicas para acelerar o desenvolvimento.

## Funcionalidades ✨

- **Laravel 12**: A aplicação está utilizando a versão mais recente do Laravel.
- **Laravel Sail**: Configuração de ambiente de desenvolvimento simplificada com Docker.
- **Laravel Octane**: Desempenho otimizado com suporte a servidores de aplicação como Swoole e RoadRunner.
- **FrankenPHP**: Integração com o servidor FrankenPHP para desempenho aprimorado.
- **Laravel Telescope**: Ferramenta de depuração para monitorar e inspecionar sua aplicação.
- **Tradução para Português**: Suporte para tradução da aplicação para o idioma português.
- **API**: Estrutura básica para criação de APIs RESTful com Laravel, incluindo autenticação e controle de acesso.
- **Supervisor**: Gerenciamento de processos para garantir que os processos do Laravel estejam sempre em execução.
- **Cron**: Configuração de tarefas agendadas para execução periódica de comandos do Laravel.
- **Laravel Horizon**: Painel de controle para gerenciar filas de trabalho com Laravel.
- **Laravel Pulse**: Ferramenta para monitoramento de métricas de desempenho em tempo real.

## Como começar 🛠️

1. Clone o repositório:
    ```sh
    git clone https://github.com/Agencia-Mop/platform.git
    ```

2. Instale as dependências:
    ```sh
    cd platform
    composer install
    ```

3. Configure o ambiente:
    ```sh
    cp .env.example .env
    php artisan key:generate
    ```

4. Inicie o ambiente de desenvolvimento:
    ```sh
    ./vendor/bin/sail up
    ```

5. Acesse a aplicação no navegador:
    ```
    http://localhost
    ```

## Contribuindo 🤝

Sinta-se à vontade para contribuir com melhorias e novas funcionalidades. Faça um fork do projeto, crie uma branch para suas alterações e envie um pull request.

---

Esperamos que esta base seja útil para seus projetos. Bons códigos! 💻
