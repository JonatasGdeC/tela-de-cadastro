# Sobre o projeto

O projeto tem como objetivo realizar a associação de clientes com seus produtos. Para isso, foi criado três telas, cada uma sendo acessada por botões encontrados na parte superior do site. São eles:

* ### Clientes e Produtos:
![Tela de cliente e produtos](./public/images/tela_cliente_produto.png)
Esta tela é reponsável por realizar as associações de clientes com os produtos. Para realizar essa associação, o usuário deve selecionar o produto na caixa de seleção do campo esquerdo do card e clicar no botão "Adicionar Produto".
<br>
Obs.: A associação só é possível caso exista no mínimo um cliente e um produto cadastrado.
<br>
<br>
* ### Clientes:
![Tela de lista e cadastro de clientes](./public/images/tela_cliente.png)
Nesta tela é realizado o cadastro de clientes, no botão "Cadastrar", e a listagem de clientes ativos e inativos.
<br>
Obs.: Quando é realizado o cadastro de um cliente, ele surge na lista como cliente ativo, sendo possível alterar esse status o que gera uma segunda lista de clientes inativos.
<br>
<br>
* ### Produtos:
![Tela de lista e cadastro de produtos](./public//images/tela_produtos.png)
Nesta tela é realizado o cadastro de produtos, no botão "Cadastrar", e a listagem de produtos ativos e inativos.
<br>
Obs.: Seguindo a mesma lógica da tela de clientes, quando é realizado o cadastro de um novo produto, ele surge na lista como produto ativo, sendo possível alterar esse status o que gera uma segunda lista de produtos inativos.
<br>
<br>

# Sobre o desenvolvimento

Ao embarcar no desenvolvimento deste projeto, fui desafiado a utilizar o VueJS, um framework com o qual tive limitado contato durante minha formação acadêmica. No entanto, com a orientação de pesquisas, documentações e as aulas do curso 'Desenvolvimento FullStack Python' da EBAC, pude explorar o VueJS de maneira acessível e clara. Vale ressaltar que o curso da EBAC recomenda a integração do VueJS com o Vite, uma ferramenta que proporciona uma construção ágil para projetos front-end. A arquitetura eficiente do Vite destaca-se pela significativa melhoria no tempo de inicialização, resultando em um desenvolvimento mais responsivo e produtivo.
<br>

A organização do projeto adota uma abordagem estruturada, onde as telas são agrupadas na pasta "containers" e os componentes específicos dessas telas são organizados na pasta "components". Essa prática favorece a modularidade e clareza, facilitando a manutenção e o entendimento do código. Além disso, a separação entre "containers" e "components" contribui para um desenvolvimento mais escalável e eficiente, promovendo uma arquitetura mais robusta e fácil de gerenciar.
<br>

Durante o desenvolvimento do projeto, uma das principais desafios enfrentados foi a gestão de dados, abrangendo informações de clientes, produtos e associações entre eles. Essa dificuldade surgiu devido à minha limitada experiência em backend. Para contornar a situação e garantir o funcionamento, optei por armazenar os dados localmente utilizando o localStorage. Embora essa solução tenha viabilizado o desenvolvimento, considerações futuras para uma abordagem de backend mais robusta podem ser exploradas para escalabilidade e segurança aprimoradas.
<br>

Para estilizar o código, foi requisitado o uso de um pré-processador CSS, levando à escolha do SASS. Este pré-processador oferece uma sintaxe robusta e organizada para a criação de folhas de estilo CSS, simplificando a manutenção e promovendo a modularidade do código. Com recursos como variáveis, mixins e aninhamento, o SASS facilita um desenvolvimento mais eficiente e legível, resultando em um código CSS mais limpo e facilmente reutilizável. Essa abordagem não apenas atende às demandas estilísticas, mas também otimiza a escalabilidade e a coesão do código de estilos.
<br>

Para assegurar a uniformidade nos códigos, foram empregadas duas ferramentas cruciais: EditorConfig e Prettier. O EditorConfig estabelece padrões de estilo entre diferentes editores, promovendo consistência em ambientes de desenvolvimento colaborativo. Complementarmente, o Prettier automatiza a formatação do código, eliminando controvérsias sobre estilos e garantindo uma apresentação uniforme, o que facilita a manutenção e reforça a legibilidade do código-fonte. A sinergia entre o EditorConfig e o Prettier fortalece a eficiência e coesão no ambiente de desenvolvimento, proporcionando benefícios tangíveis à colaboração e à manutenção do código.
<br>

Por último, para facilitar o acesso e avaliação do aplicativo, o projeto foi implantado na plataforma gratuita Vercel. Isso não apenas proporciona uma visualização prática do aplicativo, mas também permite a avaliação de seu desempenho em um ambiente real. Esse [link](https://tela-de-cadastro-pi.vercel.app/) direciona diretamente para a aplicação online, proporcionando uma experiência conveniente para os usuários avaliarem o projeto de forma eficaz.

# Para rodar o projeto

Como foi citado no último parágrafo do texto acima, foi realizado o deploy do projeto na vercel. [Link de acesso](https://tela-de-cadastro-pi.vercel.app/).
<br>
Porém, caso opte por rodar o projeto em sua máquina, você deve seguir os seguintes passos:

1. Crie uma pasta para o projeto em seu computador.
2. Abra essa pasta no VSCode e crie um novo terminal integrado do VSCode.
3. No terminal, digite os seguintes código:
<br>

```sh
git init
```
<br>

```sh
git clone https://github.com/JonatasGdeC/tela-de-cadastro.git
```
<br>
Aqui você estará criando um clone do meu projeto em sua máquina. Após isso, muito provável que irá criar uma nova pasta que irá conter o conteúdo do repositório.

<br>

4. Abra essa pasta no VSCode, crie um novo terminal e digite o seguinte código para a instalação das depedências do node.js:
<br>

```sh
npm install
```
<br>
Com isso, será instalado a pasta node_modules que contém todas as depedências necessárias para a execução do código
<br>

5. Para executar o projeto, digite no terminal o seguinte código:
```sh
npm run dev
```
