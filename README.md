# Guia Completo e Didático

## **Projeto: Sistema de Mensageria com Estruturas de Dados e RabbitMQ**

Bem-vindo ao projeto mais divertido e prático que você vai fazer no curso.
Aqui você vai aprender **estrutura de dados**, **mensageria**, **Docker**, **RabbitMQ** e **comunicação entre dispositivos**.

E tudo isso **construído do zero**, com suas próprias mãos, passo a passo.
Mesmo que você nunca tenha trabalhado com esses conceitos antes, relaxa:
este guia foi feito exatamente para você.

---

# 📌 1. O que você vai construir

Você vai criar um pequeno “WhatsApp”.
Mas bem simples.

✅ Dois dispositivos (device1 e device2)
✅ Eles enviam mensagens um para o outro
✅ Usando um servidor de mensagens real (RabbitMQ)
✅ Cada dispositivo mantém suas estruturas de dados internas:

* **Fila** (para mensagens a enviar)
* **Pilha** (para desfazer ações)
* **Lista Encadeada** (para histórico de mensagens)
* **Lista Linear** (para organizar contatos)
* **Árvore** (para organizar grupos e subgrupos)

E tudo isso será **programado por você**, do zero.
Nós só te damos a estrutura… o código é seu.

---

# 🧩 2. Como funciona a comunicação do sistema

Imagine assim:

```
device1  →  envia mensagem →  rabbitmq  →  recebe mensagem → device2
device2  →  envia mensagem →  rabbitmq  →  recebe mensagem → device1
```

### ✅ Cada device tem:

* Um **produtor** → envia mensagens para a fila do outro
* Um **consumidor** → fica escutando sua própria fila
* Suas **estruturas de dados internas**, que guardam tudo

### ✅ RabbitMQ é o "correio"

* Ele garante que a mensagem chega
* Ele enfileira a mensagem
* Ele controla mensagens pendentes / entregues

Você poderá ver isso ao vivo no painel web do RabbitMQ.

---

# 🏗️ 3. Estrutura do projeto que você precisa criar

O professor já te entrega essa estrutura vazia.
Você deve preencher **TODOS os arquivos .py**.

```
mensageria/
│
├── device.py                 ← lógica principal do device
├── debug_visual.py           ← prints bonitos (opcional)
│
├── estruturas/
│   ├── fila.py               ← implementar do zero
│   ├── pilha.py              ← implementar do zero
│   ├── lista_linear.py       ← implementar do zero
│   ├── lista_encadeada.py    ← implementar do zero
│   └── arvore.py             ← implementar do zero
│
└── services/
    ├── chat_service.py       ← integração das estruturas
    └── persistencia.py       ← salvar histórico (opcional)
```

E na raiz do projeto:

```
docker-compose.yml
Dockerfile
README.md   ← (este arquivo)
```

---

# 🐋 4. Como instalar o Docker (passo a passo simples)

Mesmo para quem nunca instalou.

---

## ✅ Windows (Docker Desktop)

1. Acesse: [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)
2. Baixe o instalador
3. Clique em “Next → Next → Install”
4. Reinicie o computador
5. Abra o Docker Desktop
6. Verifique se aparece “**Docker is running**”

---

## ✅ macOS (Docker Desktop)

1. Acesse: [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)
2. Baixe a versão para seu processador (Intel ou Apple Silicon)
3. Arraste o ícone para a pasta Applications
4. Abra o Docker Desktop
5. Verifique se está rodando

---

## ✅ Linux (Ubuntu)

Abra o terminal e execute:

```bash
sudo apt update
sudo apt install ca-certificates curl gnupg

sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" \
  | sudo tee /etc/apt/sources.list.d/docker.list

sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

Adicionar usuário no grupo docker (senão tem que usar “sudo” sempre):

```bash
sudo usermod -aG docker $USER
```

Depois reinicie o PC.

---

# ▶️ 5. Como rodar o ambiente

No terminal, dentro da pasta do projeto:

```bash
docker compose up --build
```

Pronto.
Isso vai subir:

✅ rabbitmq
✅ device1
✅ device2

---

# 🌐 6. Acessando o painel do RabbitMQ

Abra no navegador:

👉 [http://localhost:15672](http://localhost:15672)

Login:

* **Usuário:** admin
* **Senha:** admin

Aqui você vai ver:

✅ filas (queues)
✅ mensagens entrando
✅ mensagens pendentes
✅ mensagens entregues

---

# 📱 7. Como interagir com os devices

Você pode abrir o terminal de cada device:

```bash
docker exec -it device1 bash
docker exec -it device2 bash
```

Ou acompanhar os logs ao vivo:

```bash
docker logs -f device1
docker logs -f device2
```

---

# ⌨️ 8. Comandos dentro do dispositivo

| Comando   | O que faz                          |
| --------- | ---------------------------------- |
| `<texto>` | envia mensagem                     |
| `/hist`   | mostra histórico (lista encadeada) |
| `/fila`   | mostra fila local                  |
| `/undo`   | desfaz última ação (pilha)         |
| `/exit`   | sai                                |
| `/help`   | mostra ajuda                       |

---

# 🧠 9. O que você (aluno) precisa desenvolver

Você deve implementar **TODAS as estruturas de dados**, usando **somente ponteiros, nós, e lógica manual**.

Nada de `list.append`, `list.pop`, `deque`, nada disso.

### ✅ 1. Fila (queue)

* `enfileirar`
* `desenfileirar`
* `remover`
* `mostrar`

### ✅ 2. Pilha (stack)

* `empilhar`
* `desempilhar`
* `mostrar`

### ✅ 3. Lista Encadeada

* `adicionar`
* `remover`
* `procurar`
* `mostrar`

### ✅ 4. Lista Linear (array manual)

* `adicionar`
* `inserir`
* `remover`
* `buscar`
* `mostrar`

### ✅ 5. Árvore

* `adicionar`
* `buscar`
* `mostrar`

### ✅ 6. chat_service.py

Aqui você faz:

* enviar mensagem
* receber mensagem
* registrar no histórico
* inserir na fila
* empilhar no undo

### ✅ 7. device.py

Aqui você implementa:

* interface do usuário
* comandos (`/hist`, `/fila`, `/undo`)
* envio de mensagens
* consumo de mensagens

---

# ✅ 10. Checklist para o aluno (seguir na ordem)

**✅ 1. Instalar o Docker**
**✅ 2. Rodar `docker compose up`**
**✅ 3. Testar rabbitmq na porta 15672**
**✅ 4. Entrar no device e testar digitar mensagens**
**✅ 5. Implementar fila completa**
**✅ 6. Implementar pilha completa**
**✅ 7. Implementar lista encadeada**
**✅ 8. Integrar no `chat_service.py`**
**✅ 9. Implementar lista linear**
**✅ 10. Implementar árvore**
**✅ 11. Criar grupos de contatos**
**✅ 12. Criar funções extras (opcional)**

* salvar histórico
* auto-resposta
* broadcast
* estatísticas da fila

---

# 🧪 11. Como testar se está funcionando

### ✅ Teste 1: device1 envia para device2

No terminal do `device1`:

```
Olá device2!
```

No terminal do `device2` deve aparecer:

```
📩 Recebido de device1: Olá device2!
```

### ✅ Teste 2: fila local funciona

```
/fila
```

### ✅ Teste 3: histórico funciona

```
/hist
```

### ✅ Teste 4: desfazer funciona

```
/undo
```

---

# 🧯 12. Problemas comuns e soluções

### ✅ “docker: command not found”

→ Docker não instalado corretamente.
→ Releia a seção de instalação da sua plataforma.

### ✅ RabbitMQ não sobe

Rode:

```bash
docker compose down
docker compose up --build
```

### ✅ device1 não recebe mensagens

Verifique no RabbitMQ se a fila **device1** existe.

---

# ✅ 13. Final

Esse projeto vai te ensinar:

✅ Estruturas de dados
✅ Programação Python real
✅ Conceitos modernos de mensageria
✅ Trabalho em equipe
✅ Como sistemas reais funcionam

Divirta-se construindo.
Pergunte sempre.
E lembre-se: **errar faz parte do aprendizado**.
