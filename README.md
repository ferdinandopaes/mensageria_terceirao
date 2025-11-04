# Mensageria III Termo ADS - Estrutura de Dados + RabbitMQ

## 📌 1. Sobre o projeto

Este projeto é uma atividade prática desenvolvida para aprender **estruturas de dados fundamentais** enquanto construímos um **sistema de mensageria** inspirado em um chat simples (tipo WhatsApp).

Tudo é simulado **localmente**, mas usando elementos reais como:

✅ **RabbitMQ** – fila real de mensagens
✅ **Docker + Docker Compose** – ambiente containerizado
✅ **Dois dispositivos** (device1 e device2) trocando mensagens
✅ **Modo debug visual** mostrando as estruturas funcionando

---

## 🎯 2. Objetivo educacional

A ideia é que o aluno aprenda, na prática:

### ✅ Estruturas de dados implementadas do zero

* **Fila (Queue)**
* **Pilha (Stack)**
* **Lista linear**
* **Lista encadeada (Linked List)**
* **Árvore (Tree)**

### ✅ Conceitos de mensageria

* Produtor / consumidor
* Enfileiramento
* ACK
* Mensagens pendentes vs entregues

### ✅ Integração com software real

* Como um sistema real usa estruturas de dados internamente
* Como ferramentas como WhatsApp/Telegram funcionam por baixo dos panos
* Funcionamento básico de um broker de mensagens (RabbitMQ)

---

## 🧱 3. Arquitetura

```
docker-compose.yml
│
├── rabbitmq          → fila de mensagens (broker)
│
└── mensageria/
    ├── device.py     → código principal do dispositivo
    ├── debug_visual.py
    ├── estruturas/
    │   ├── fila.py
    │   ├── pilha.py
    │   ├── lista_linear.py
    │   ├── lista_encadeada.py
    │   └── arvore.py
    └── services/
        ├── chat_service.py
        └── persistencia.py
```

---

## 🚀 4. O fluxo do sistema

Cada dispositivo executa:

1. ✅ Um **produtor** → envia mensagens para o outro device

2. ✅ Um **consumidor** → recebe mensagens enviadas ao seu nome

3. ✅ Um conjunto de **estruturas internas**, todas implementadas manualmente:

   * Fila local de mensagens enviadas
   * Pilha de UNDO
   * Lista encadeada de histórico
   * Árvore (a ser implementada pelos alunos)
   * Lista linear (para funcionalidades extras)

4. ✅ Um **modo debug** — mostra:

   * Quando a mensagem foi enfileirada
   * Quando foi enviada
   * Quando foi recebida
   * Como está a fila local em tempo real

---

## 🧰 5. Como instalar o Docker

### 🔹 Windows

1. Baixe o Docker Desktop:
   [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)
2. Instale e reinicie o computador
3. Abra o Docker Desktop e verifique se está rodando

---

### 🔹 Linux (Ubuntu/Debian)

```bash
sudo apt update
sudo apt install ca-certificates curl gnupg

sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" \
  | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update

sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Adicionar o usuário ao grupo docker:

```bash
sudo usermod -aG docker $USER
```

**Reinicie a máquina depois disso.**

---

### 🔹 macOS

✅ Recomendado: Docker Desktop
[https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)

Após instalar, abra o aplicativo e certifique-se de que está rodando.

---

## 🐋 6. Como rodar o ambiente (Docker Compose)

1. Entre na pasta do projeto:

```bash
cd mensageria_full
```

2. Suba o ambiente:

```bash
docker compose up --build
```

3. O sistema subirá:

* `rabbitmq` → broker
* `device1` → primeiro dispositivo
* `device2` → segundo dispositivo

4. Acesse o painel do RabbitMQ:

👉 **[http://localhost:15672](http://localhost:15672)**
Usuário: `admin`
Senha: `admin`

Aqui os alunos conseguem visualizar:

✅ Filas
✅ Mensagens entrando e saindo
✅ Mensagens pendentes
✅ Mensagens entregues
✅ Quantidade de mensagens por segundo

---

## 📱 7. Como usar os dispositivos (device1 e device2)

Quando os containers subirem, abra dois terminais:

Para acompanhar o device1:

```bash
docker logs -f device1
```

Para acompanhar o device2:

```bash
docker logs -f device2
```

Ou abra um shell interativo:

```bash
docker exec -it device1 bash
docker exec -it device2 bash
```

Dentro do prompt, os comandos são:

| Comando   | Função                                  |
| --------- | --------------------------------------- |
| `<texto>` | envia mensagem para o outro dispositivo |
| `/hist`   | mostra o histórico (lista encadeada)    |
| `/fila`   | mostra fila local                       |
| `/undo`   | desfaz última operação (pilha)          |
| `/exit`   | sai                                     |
| `/help`   | mostra ajuda                            |

---

## 🧑‍💻 8. O que devem desenvolver

### ✅ Implementações completas:

* Fila 
* Pilha 
* Lista encadeada 
* Lista linear 
* Árvore 

### ✅ O que eles devem entender:

* A diferença entre fila e fila do RabbitMQ
* Como o chat simula a lógica interna
* Como a pilha funciona com UNDO
* Como o histórico se forma com lista encadeada

### ✅ Podem evoluir implementando:

* Busca por mensagens na lista encadeada
* Organização dos contatos com árvore
* Threads respondendo mensagens automaticamente
* Persistência (armazenar conversas em JSON)
* UI simples em linha de comando, etc.

---

## 🧭 9. Sugestão de etapas para os alunos

### 1

→ Instalar Docker
→ Subir o ambiente
→ Entender a arquitetura
→ Testar envio e recebimento

### 2


---

## ✅ 10. Finalizando

Esse projeto:

✅ Mostra estruturas de dados **na prática**, não só na teoria
✅ Usa ferramenta real do mercado (RabbitMQ)
✅ Permite visualização do fluxo real
✅ Ajuda os alunos a construir raciocínio de arquitetura
✅ Dá autonomia e abre portas para aprendizado avançado
