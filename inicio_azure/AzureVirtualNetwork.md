# Iniciando a aplicação
- Para iniciar, entre na maquina e execute a aplicação
- entre na máquina
```
ssh -i chave.pem azureuser@40.88.140.65
```
- entre dno diretório da aplicação
```
cd 1862-sequelize/api
```

- Rode a aplicação
```
node index.js
```

# Aprendendo a criar uma VNET da Azure
- No portal da azure, clique em "Criar um recurso"
- Procure por "Virtual network"
- Clique em "Virtual network"
- Clique no botão "Criar" 


* Configurando a Vnet
- Selecione sua assinatura e grupo de recurso
- Selecione um  nome para a rede Virtual
- Mantém a região US East US, ou outra região que foi definido seu grupo de recurso
- Avançar para segurança, deixe como esta e avance para Endereços Ips, deixe como esta, Avance para marcas, selecione env e dev
- Clique em Revisar + Criar
- Clique em criar
- é possível criar uma vnet utilizando CLI da azure
- no terminal da azure, clique no terminal e escolha bash
```
az network vnet create --name rede-criada-pelo-cli --resource-group cristhian_curso_alura --address-prefix 10.0.0.0/16
```


* Criando Subnets
- Pesquise pelo recurso no centro superior da tela, por "Redes virtuais"
- Selecione a rede virtual que esta usando o backend, a api da aplicação
- No menu lateral esquerdo, clique em Sub-redes
- Clique no botão "+ Sub-rede" para criar uma nova subrede
- Na janela de criação da subrede, preencha os campos necessários
- Defina apenas o nome e clique em "Adicionar"


* Criando uma nova máquina de frontend
- Crie uma nova máquina, seguindo os mesmos passos do readme VM.md
- na parte de rede no campo Rede virtual, selecione a  rede default 
- no campo subrede, selecione a subrede criada anteriormente
- com a maquina criada, entre via shh e atualize a máquina com update e dist-upgrade
- crie um diretório chamado front, entre nele e instale:
```
sudo apt-get install nodejs
sudo apt-get install npm
```
- inicie o ambiente
```
npm init
```
- Aperte "Enter" Para todas as perguntas
- instale o pacote express do npm
```
npm install express
```

- instale o pacote axios
```
npm install axios
```



* Instalando a aplicação frontend
- na pasta front, digite:
```
nano index.js
```
- cole no index.js:
```
const express = require('express');
const axios = require('axios');
const app = express();
const port = 5000;
app.get('/', (req, res) => {
    const url = 'xxx/turmas';
    console.log(`Acessando o back-end em: ${url}`);
    axios.get(url)
    .then(response => {
        const turmas = response.data;
        res.send(`Olá, eu sou o front-end. Esta foi a resposta do backend: ${JSON.stringify(turmas)}`);
    })
    .catch(error => {
        console.log(error);
        res.send(error);
    });
});
app.listen(port, () => {
    console.log(`Servidor está rodando em http://localhost:${port}`);
});
```

- modifique a variável cont url, atribua um valor de http://ip-publico-da-outra-vm:3000/turmas
- salve com ctrl+s e ctrl+x para salver e sair do nano

- libere a porta 5000 da VM
- Vá até a VM que esta rodando o frontend, no menu lateral esquerdo, selecione "Configurações de Rede"
- Em Configurações de Rede, crie uma regra de portas de entrada e saída para a porta 5000, libere esta porta. Mude de 8080 para 5000
- entre na URL: http://ip-maquina-front:5000/
- se retornar a mensagem abaixo, deu tudo certo:
```
Olá, eu sou o front-end. Esta foi a resposta do backend: [{"id":1,"data_inicio":"2021-10-17","createdAt":"2021-10-17","updatedAt":"2021-10-17","nivel_id":1,"docente_id":1}]
```


# Grupo de segurança de rede
- No momento que está, conseguimos conectar na maquina de backend e frontend, mas não é nada viável acessar uma máquina backend, então neste tópico abordei sobre recusar acesso na maquina backend pelo navegador
- Abra a máquina backend pelo portal da azure
- no menu lateral esquerdo, clique em configuração de redes
- Clique na configuração de porta de entrada 3000
- no campo Origem, selecione Ip Addresses
- no campo Intervalors de CIDR/endereço IP de origem, adicione o IP público da VM frontend
- clique em salvar
- Pronto, agora não é mais possivel acessar a maquina de backend pelo navageador, apenas a maquina frontend esta permitida para acessar a maquina backend
