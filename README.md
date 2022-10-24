# Trabalho-ES---Arquitetura-Serverless
Exemplo prático de Arquitetura Serverless

Essa atividade prática foi desenvolvida pelo Grupo 7:
- **Bruno Rocha Ribeiro**
- **Eduardo Vinicius Silva de Lima**
- **Italo Gustavo Donato Cordeiro**
- **Rosane Silva Freitas Araujo**

O modelo de arquitetura Serverless é uma espécie de desenvolvimento nativo em nuvem para criação e execução de aplicações sem o gerenciamento de servidores.

Porém, é válido citar que os servidores ainda são usados nesse modelo, apesar dos mesmos serem abstraídos durante o desenvolvimento de aplicações. Sendo assim, um provedor de nuvem passa a ser o responsável pelas tarefas que fazem o provisionamento, a manutenção e também a escala da infraestrutura do servidor, ficando a encargo dos desenvolvedores a etapa de empacotar o código em containers e então realizar sua implementação.

Após realizada a implementação, as aplicações serverless devem ser capazes de suprir a demanda, podendo aumentar ou diminuir a escala automaticamente de acordo com as necessidades. 

Baseamos então a prática pelo [projeto](https://github.com/tiagoboeing/youtube-serverless-framework-lambda-api-gateway) de estudo de um [especialista](https://www.linkedin.com/in/tiagoboeing/) em AWS.

 ## 1.  Instalação do Framework

Para essa prática, será usado o framework [serverless](serverless.com), que deve ser instalado com o comando:
```
npm i -g serverless
```

![image](https://user-images.githubusercontent.com/54030641/197426400-19283712-5748-4bd6-8399-266314a0e9ef.png)

Para verificar se a instalação foi concluída com sucesso, basta rodar o comando 
```
serverless
```

No caso se tudo estiver correto ele vai oferecer a opção d criar um novo projeto serveless

![image](https://user-images.githubusercontent.com/54030641/197426498-02398bac-5cbf-4784-84d6-fdcbeec8f554.png)

 ## 2.  Criação do projeto

Abra a pasta na qual o seu projeto ficará armazenado e rode o comando
```
npm init -y
```
![image](https://user-images.githubusercontent.com/54030641/197426594-06a35bfd-409b-45ad-80b7-9edcc90d8ab5.png)

Logo em seguida, para instalar o framework no seu projeto, rode
```
npm i serverless -D
```

![image](https://user-images.githubusercontent.com/54030641/197426741-7161d12e-41c1-414a-a3d8-209bc5d992c9.png)

Após a instalação o pacote apareceça no seu package.json em devDependencies

![image](https://user-images.githubusercontent.com/54030641/197426869-1103355e-c4c5-4dcb-8de9-2b76186db40b.png)

Para trabalhar com o serverless é necessário criar um arquivo com o nome “serverless.yml” na raiz do projeto.

Obs : Para este roteiro funcionar, é necessário configurar as credenciais da aws. Para mais informações, acesse o (site)[https://www.serverless.com/framework/docs/providers/aws/guide/credentials/
]

Insira o seguinte trecho de código no arquivo criado:
```
service: sls-my-first-lambda

provider:
  name: aws
  runtime: nodejs//+versão node
  stage: ${opt:stage, 'dev'}
  region: ${opt:region, 'us-east-1'}
  memorySize: 128
  timeout: 3
```
```
functions:
  index:
  handler: index.handler
  description: My first lambda example
  events:
    - http:
      path: / //+rota
      method: get
      cors: true
```

Agora, para implementar a função handler, vamos criar um arquivo index.js com o seguinte código:
```
exports.handler = async function
handler(event, context) {
return {
statusCode: 200,
body: JSON.stringify({ message: 'My first lambda' })
};
};
```
  ## 3.  Rodando o projeto
Para rodar o projeto, basta, no terminal, rodar o comando
```
serveless deploy 
```

Pronto! Agora basta entrar na aws, em CloudFormation, e verificar sua stack criada! Para testar sua lambda, vá para Lambda em code e clique em Test.

