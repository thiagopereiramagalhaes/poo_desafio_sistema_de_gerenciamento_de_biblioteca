# Desafio POO: Sistema de Gerenciamento de Biblioteca
Imagine que você está criando um sistema de gerenciamento de biblioteca em Python. **Seu objetivo é criar três classes**: *`Livro`*, *`Cliente`* e *`Biblioteca`*, **negrito** **cada uma com métodos apropriados**. Aqui está a descrição de cada classe:

1. **Livro:**
* [X] A classe Livro deve ter os seguintes atributos: título, autor, ano de publicação e número de cópias disponíveis.
* [X] Deve ter um método chamado emprestar() que reduz o número de cópias disponíveis em 1 sempre que um livro é emprestado.
* [X] Deve ter um método chamado devolver() que aumenta o número de cópias disponíveis em 1 sempre que um livro é devolvido.
* [X] Deve ter um método disponivel() que retorna True se houver pelo menos uma cópia disponível, e False caso contrário.

2. **Cliente:**

* [X] A classe Cliente deve ter os seguintes atributos: nome, número de identificação do cliente e lista de livros atualmente em posse do cliente.
* [X] Deve ter um método pegar_livro(livro) que permite que o cliente pegue emprestado um livro, desde que o livro esteja disponível na biblioteca.
* [X] Deve ter um método devolver_livro(livro) que permite que o cliente devolva um livro.
* [X] Deve ter um método livros_em_posse() que retorna a lista de livros atualmente em posse do cliente.

3. **Biblioteca:**

* [X] A classe Biblioteca deve ter uma lista de livros disponíveis e uma lista de clientes registrados.
* [X] Deve ter um método adicionar_livro(livro) que permite adicionar um livro à biblioteca.
* [X] Deve ter um método adicionar_cliente(cliente) que permite registrar um cliente na biblioteca.
* [X] Deve ter um método emprestar_livro(cliente, livro) que permite a um cliente emprestar um livro da biblioteca.
* [X] Deve ter um método listar_livros_disponiveis() que retorna a lista de livros disponíveis na biblioteca.
* [X] Deve ter um método listar_clientes() que retorna a lista de clientes registrados na biblioteca.

**Seu desafio é implementar essas três classes e os métodos descritos acima, garantindo que eles funcionem corretamente.** Você também pode adicionar métodos adicionais ou funcionalidades se desejar. Boa sorte!

***Fonte***: https://chat.openai.com/

***Código***: https://colab.research.google.com/drive/1c-y_e3Fsy3FomphMzBnIRtq1y2Fgp3Uv?usp=sharing

```python
class Livro:
  def __init__(self, titulo, autor, ano, copias_disponiveis):
    self.titulo = titulo
    self.autor = autor
    self.ano = ano
    self.copias_disponiveis = copias_disponiveis
  
  def emprestar(self):
    if self.copias_disponiveis > 0:
      self.copias_disponiveis -= 1
      return True
    else:
      return False

  def devolver(self):
    self.copias_disponiveis += 1

  def disponivel(self):
    return self.copias_disponiveis > 0
```

```python
class Cliente:
  def __init__(self, nome, identificacao):
    self.nome = nome
    self.id_cliente = identificacao
    self._livros_em_posse = []

  def pegar_livro(self, livro):
    self._livros_em_posse.append(livro)

  def devolver_livro(self, livro):
    if livro in self._livros_em_posse:
      self._livros_em_posse.remove(livro)
      return True
    else:
      return False

  def livros_em_posse(self):
    return [livro.titulo for livro in self._livros_em_posse]
```

```python
class Biblioteca:
  def __init__(self):
    self.livros_disponiveis = []
    self.clientes_registrados = []

  def adicionar_livro(self, livro):
    self.livros_disponiveis.append(livro)

  def adicionar_cliente(self, cliente):
    self.clientes_registrados.append(cliente)

  def emprestar_livro(self, cliente, livro):
    if cliente in self.clientes_registrados and livro in self.livros_disponiveis:
      if livro.emprestar():
        cliente.pegar_livro(livro)
        self.livros_disponiveis.remove(livro)
        return True
      else:
        return False
    else:
      return False

  def listar_livros_disponiveis(self):
    return [livro.titulo for livro in self.livros_disponiveis]

  def listar_clientes(self):
    return [cliente.nome for cliente in self.clientes_registrados]
```

```python
livros= [
    {"titulo": "A Guerra dos Tronos", "autor": "George R.R. Martin", "ano": 1996, "copias": 3},
    {"titulo": "1984", "autor": "George Orwell", "ano": 1949, "copias": 5},
    {"titulo": "O Senhor dos Anéis", "autor": "J.R.R. Tolkien", "ano": 1954, "copias": 2},
    {"titulo": "O Pequeno Príncipe", "autor": "Antoine de Saint-Exupéry", "ano": 1943, "copias": 4},
    {"titulo": "Harry Potter e a Pedra Filosofal", "autor": "J.K. Rowling", "ano": 1997, "copias": 6},
]
clientes = [
    {"nome": "Alice", "identificacao": 123},
    {"nome": "Bob", "identificacao": 456},
    {"nome": "Carol", "identificacao": 789},
    {"nome": "David", "identificacao": 101},
    {"nome": "Eve", "identificacao": 202},
]
```

```python
biblioteca = Biblioteca()
for livro in livros:
  biblioteca.adicionar_livro(Livro(livro['titulo'], livro['autor'], livro['ano'], livro['copias']))

print(biblioteca.listar_livros_disponiveis())
```

```python
for cliente in clientes:
  biblioteca.adicionar_cliente(Cliente(cliente['nome'], cliente['identificacao']))

print(biblioteca.listar_clientes())
```
