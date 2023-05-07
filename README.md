FORMAT: 1A
HOST: https://localhost:8000/

# EcommerceBook-API

A API permitirá ao usuário acessar informações sobre autores e livros do banco de dados ecommercebook, incluindo a criação, atualização e exclusão de registros de livros, bem como a consulta de informações de um livro específico.
##Coleção Autores [/autores]
###Listar todos os autores [GET]

Lista todos os autores

+ Response 200 (application/json)

    + Body

            [
                {
                    "id": 1,
                    "nome": "Autor 1"
                },
                {
                    "id": 2,
                    "nome": "Autor 2"
                }
            ]
###Cria um novo autor [POST]

Cria um novo autor.

+ Request (application/json)

            {
              "nome": "Autor 3"
            }

+ Response 201 (application/json)
        + Headers
            Location: /autores/3
            
    + Body

            {
                "id": 3,
                "nome": "Autor 3"
            }

## Atualiza/Remove um item da coleção [/autores/{id}]

+ Parameters
    + id (number) - ID do registro a ser atualizado, formato de numero inteiro

###Obter um autor [GET]

Retorna as informações de um autor.

+ Parameters
    + id (number) - ID do autor a ser recuperado.

+ Response 200 (application/json)

    + Body

            {
              "id": 2,
              "nome": "Autor 2"
            }

+ Response 404 (application/json)

    + Body

                {
                  "message": "Autor não encontrado."
                }
          

###Atualiza um autor [PUT]

Atualiza as informações de um autor.

+ Parameters
    + id (number) - ID do autor a ser atualizado.

+ Request (application/json)

            {
              "nome": "Autor 2 atualizado"
            }

+ Response 200 (application/json)

    + Body

            {
              "message": "Autor atualizado com sucesso."
            }

+ Response 404 (application/json)

    + Body

            {
              "message": "Autor não encontrado."
            }

###Remove um autor [DELETE]

Remove um autor e todos os livros associados.

+ Parameters
    + id (number) - ID do autor a ser removido.

+ Response 200 (application/json)

    + Body


            {
              "message": "Autor removido com sucesso."
            }

+ Response 404 (application/json)

    + Body
    
            {
              "message": "Autor não encontrado."
            }

##Livros [/livros]
###Listar todos os livros [GET]

+ Response 200 (application/json)

            [
                {
                    "id": 1,
                    "titulo": "Livro 1",
                    "preco": "50.00",
                    "urlImage": "https://exemplo.com/imagem1.jpg",
                    "genero": "Ação",
                    "dataLancamento": "2022-05-01",
                    "autor": {
                        "id": 1,
                        "nome": "Autor 1"
                    }
                },
                {
                    "id": 2,
                    "titulo": "Livro 2",
                    "preco": "35.00",
                    "urlImage": "https://exemplo.com/imagem2.jpg",
                    "genero": "Romance",
                    "dataLancamento": "2021-10-15",
                    "autor": {
                        "id": 2,
                        "nome": "Autor 2"
                    }
                }
            ]
###Cria um novo livro [POST]

Você pode criar um novo livro por meio desta ação.

+ Request (application/json)

    + Body
    
           
            {
                "titulo": "Livro 3",
                "preco": "27.90",
                "urlImage": "https://exemplo.com/imagem3.jpg",
                "genero": "Ficção Científica",
                "dataLancamento": "2023-02-28",
                "autor_id": 1
            }
  

+ Response 201 (application/json)

        + Headers
            Location: /livros/3

    + Body

            {
                "id": 3, //informar ID aqui e nao utilizar Location acima
                "titulo": "Livro 3",
                "preco": "27.90",
                "urlImage": "https://exemplo.com/imagem3.jpg",
                "genero": "Ficção Científica",
                "dataLancamento": "2023-02-28",
                "autor": {
                    "id": 1,
                    "nome": "Autor 1"
                }
            }

+ Response 400 (application/json)

    + Body


            {
                "message": "campos obrigatórios não informados",
            }
      

+ Response 415 (application/json)

    + Body

            {
                "message": "os dados devem ser informados em JSON",
            }

###Consultar um livro [GET /livros/{id}]

+ Parameters
    + id (number) - ID do livro a ser consultado, formato de numero inteiro

+ Response 200 (application/json)

    + Body

            {
                "id": 1,
                "titulo": "Livro 1",
                "preco": "50.00",
                "urlImage": "https://exemplo.com/imagem1.jpg",
                "genero": "Ação",
                "dataLancamento": "2022-05-01",
                "autor": {
                    "id": 1,
                    "nome": "Autor 1"
                }
            }

+ Response 404 (application/json)

    + Body

            {
              "message": "livro não encontrado",
            }

## Atualiza/Remove um item da coleção [/livros/{id}]

+ Parameters
    + id (number) - ID do registro a ser atualizado, formato de numero inteiro

###Atualizar um livro [PUT]

Atualiza as informações de um livro existente.

+ Parameters
       + id (number) - ID do registro a ser atualizado, formato de numero inteiro
        

            {
              "titulo": "Novo Título",
              "preco": "30.00",
              "urlImage": "https://exemplo.com/imagem2.jpg",
              "genero": "Drama",
              "dataLancamento": "2023-01-01",
              "autor_id": 2
            }

    
+ Response 200 (application/json)

    + Body


            {
                "id": 1,
                "titulo": "Novo Título",
                "preco": "30.00",
                "urlImage": "https://exemplo.com/imagem2.jpg",
                "genero": "Drama",
                "dataLancamento": "2023-01-01",
                "autor": {
                    "id": 2,
                    "nome": "Autor 2"
                }
            }

+ Response 404 (application/json)


    + Body

            {
                "message": "livro não encontrado",
            }

###Excluir um livro [DELETE]

+ Parameters
    + id (number) - ID do livro a ser excluído, formato de numero inteiro
    
+ Response 204
