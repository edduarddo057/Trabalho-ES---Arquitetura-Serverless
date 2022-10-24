# Trabalho-ES---Arquitetura-Serverless
Exemplo prático de Arquitetura Serverless

Essa atividade prática foi desenvolvida pelo Grupo 7:
- **Bruno Rocha Ribeiro**
- **Eduardo Vinicius Silva de Lima**
- **Italo Gustavo Donato Cordeiro**
- **Rosane Silva Freitas Araujo**

A atividade foi projetada para ser usada como os exemplos de prática da disciplina de Engenharia de Software. Nos baseamos no [livro](https://www.amazon.com.br/Serverless-Architectures-AWS-Peter-Sbarski/dp/1617293822) do Peter Sbarski - Serverless Architectures on AWS: With Examples Using AWS Lambda. 

Serverless é um modelo de desenvolvimento nativo em nuvem para criação e execução de aplicações sem o gerenciamento de servidores.

Os servidores ainda são usados nesse modelo, mas eles são abstraídos do desenvolvimento de aplicações. O provedor de nuvem fica responsável pelas tarefas rotineiras de provisionamento, manutenção e escala da infraestrutura do servidor. Os desenvolvedores só precisam empacotar o código em containers para fazer a implantação.

Depois da implantação, as aplicações serverless atendem à demanda e aumentam ou diminuem a escala automaticamente de acordo com as necessidades. As soluções serverless dos provedores de nuvem pública costumam ser oferecidas sob demanda por meio de um modelo de execução orientado a eventos. Por isso, não há cobrança pelas funções serverless não utilizadas.

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

