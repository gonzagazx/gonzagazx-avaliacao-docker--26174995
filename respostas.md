# Respostas · Avaliação Prática de Docker · ViaSerra Transportes (Turma C)

Nome: Matheus Gonzaga
Matrícula: 26174995
Usuário do GitHub: gonzagazx
Usuário do Docker Hub: gonzagazx

Responda com as suas palavras e com o que aconteceu na SUA máquina. Resposta curta e certa vale mais
do que texto longo copiado. Resposta que contradiz o seu próprio Dockerfile vale zero.

## Parte 1 · Dockerfile do portal

1. Qual imagem base você usou e qual o tamanho final da imagem do portal (saída de `docker images`)?
R:A imagem base utilizada foi nginx:1.29.2. O tamanho final da imagem do portal é: 224.86 MB

2. Em qual pasta do container o Nginx procura os arquivos do site? Mostre o comando que você usou para
   conferir que o `index.html` está lá dentro.
R:O Nginx procura os arquivos do site na pasta /usr/share/nginx/html/.
O comando utilizado foi: docker exec teste-portal ls -l /usr/share/nginx/html/index.html

## Parte 2 · Docker Hub

3. Nome completo da imagem publicada e link público do repositório no Docker Hub.
R: https://hub.docker.com/r/gonzagazx/viaserra-portal

4. Se você mudar o HTML, quais comandos precisa rodar para que a versão nova chegue ao Docker Hub?
R: Se eu alterar o HTML, preciso reconstruir a imagem, usar uma nova tag, fazer o push para o Docker Hub.

## Parte 3 · Página de manutenção

5. 	
R:
Instrução	O que estava errado	O que você viu acontecer	Como corrigiu
1	COPY pagina/ .	A pasta pagina/ não existia no projeto.	O docker build falhou informando que /pagina não foi encontrado.	Alterei para COPY site/ ....
2	COPY site/ .	Os arquivos eram copiados para /usr/share/nginx/, e não para a pasta que o Nginx utiliza para servir o site.	O container iniciava, mas a página não era disponibilizada corretamente.	Alterei para COPY site/ /usr/share/nginx/html/.
3	CMD ["nginx"]	O Nginx era iniciado em segundo plano, fazendo o processo principal do container terminar.	O Nginx aparecia nos logs como iniciado, mas o container encerrava com código 0.	Alterei para CMD ["nginx", "-g", "daemon off;"].

6. Qual a diferença entre `-p 7042:80` e `-p 80:7042` no `docker run`? Qual dos dois números é a porta do container?
R: -p segue a ordem. A porta do container é sempre o segundo conjunto de numero

-p 7042:80 - computador 7042 - container 80
-p 80:7042 - computador 80 - container 7042
A porta do container é sempre o segundo conjunto de numero



## Parte 4 · Primeiro docker-compose

7. Escreva os dois comandos `docker run` que fariam o mesmo que o seu `docker-compose.yml`.
R: docker run -d -p 8095:80 gonzagazx/viaserra-portal:1.0-26174995
docker run -d -p 7095:80 manutencao:26174995

8. Qual comando derruba os dois containers de uma vez?
R:docker compose down

## Verificador

9. Código de conclusão impresso pelo verificador:
R:VIASERRA-26174995-6EF9DA1B
```
(cole aqui)
```
