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

## Jobs e Filas ⚙️

Esta aplicação utiliza o Laravel para gerenciar jobs e filas, e o Supervisor para gerenciar os workers que processam essas filas. O worker padrão está configurado para processar a fila `default`.

### Configuração do Worker

O arquivo de configuração do Supervisor (`laravel-worker.conf`) define um worker que processa a fila `default`:

```properties
[program:laravel-worker]
process_name=%(program_name)s_%(process_num)02d
command=php /app/artisan queue:work --sleep=3 --tries=5 --timeout=3600
autostart=true
autorestart=true
stopasgroup=true
killasgroup=true
user=www-data
numprocs=8
redirect_stderr=true
stdout_logfile=/app/supervisor/worker.log
stopwaitsecs=3600
```

### Adicionando Novas Filas

Para adicionar novas filas, você precisa criar novos workers no Supervisor com o nome específico da fila que deseja processar. Por exemplo, para adicionar um worker para a fila `emails`, você pode criar um novo arquivo de configuração do Supervisor:

```properties
[program:laravel-worker-emails]
process_name=%(program_name)s_%(process_num)02d
command=php /app/artisan queue:work --queue=emails --sleep=3 --tries=5 --timeout=3600
autostart=true
autorestart=true
stopasgroup=true
killasgroup=true
user=www-data
numprocs=1
redirect_stderr=true
stdout_logfile=/app/supervisor/worker-emails.log
stopwaitsecs=3600
```

Depois de adicionar o novo arquivo de configuração, recarregue o Supervisor:

```sh
supervisorctl reread
supervisorctl update
supervisorctl start "laravel-worker-emails:*"
```

## Agendamentos (Schedule) 🗓️

Esta aplicação utiliza o cron para gerenciar os agendamentos definidos no Laravel. O cron é configurado para executar o comando `schedule:run` a cada minuto, garantindo que todas as tarefas agendadas sejam executadas conforme definido no arquivo `App\Console\Kernel.php`.

### Configuração do Cron

O arquivo de configuração do cron (`/etc/cron.d/laravel-scheduler`) é definido da seguinte forma:

```sh
* * * * * cd /app && php artisan schedule:run >> /dev/null 2>&1
```

Este comando garante que o Laravel execute todas as tarefas agendadas a cada minuto.

### Adicionando Novas Tarefas Agendadas

Para adicionar novas tarefas agendadas, edite o arquivo `App\Console\Kernel.php` e adicione suas tarefas ao método `schedule`:

```php
protected function schedule(Schedule $schedule)
{
    // Exemplo de tarefa agendada
    $schedule->command('emails:send')->daily();
}
```

Depois de adicionar suas tarefas, o cron garantirá que elas sejam executadas conforme o agendamento definido.

## Contribuindo 🤝

Sinta-se à vontade para contribuir com melhorias e novas funcionalidades. Faça um fork do projeto, crie uma branch para suas alterações e envie um pull request.

---

Esperamos que esta base seja útil para seus projetos. Bons códigos! 💻
