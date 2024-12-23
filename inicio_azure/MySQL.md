## A aplicação que vai ser utilizada, requer o uso de um banco de dados MYSQL, então vou criar um recurso da AZURE de banco de dados
- Vá em criar um recurso
- Procure por Banco de dados, e clique no recurso.
- Pesquise por "Azure Database for MySQL" e selecione-o
- Em Servidor flexível, clique em "advanced Create"

* Redes
- Na parte de redes, marque a opção de Acesso Público e Regras de Firewall
- Adicione o endereço IP do cliente atual, e 0.0.0.0
- Clique em Avançar: Segurança
- Clique em Avançar: Rotulos
- Selecione o nome e valor: env e dev
- Clique em Avançar: Revisar + Criar
- Clique em Criar
- Aguarde a criação do recurso

* Configuração básica
- Preencha as informações


## Criando um banco de dados
- Com a máquina logada, é necessário ter o mysql instalado, para instalar siga esses passos:
```bash
sudo apt install mysql-client-core-8.0
mysql --version
```
- Depois que instalado, é esperado que apareça a seguinte mensagem:
```bash
mysql  Ver 8.0.31-0ubuntu0.20.04.2 for Linux on x86_64 ((Ubuntu))Copiar c
```


- Volte ao grupo de recursos, clique no serviço banco de dados criado, no menu lateral esquerdo procure por "Parâmetros do servidor"
- Em "Parâmetros do servidor", procure por ssl e o valor defina para OFF e clique em salvar, aguarde a implantação for concluída.
- Com a implantação concluída, clique em Banco de dados, clique em Adicionar
- Preencha as informações para criar o banco de dados e clique em salvar, aguarde a criação do banco de dados



* Como logar no banco de dados criado?
- Como recurso selecionado, clique em "Conectar" para verificar os detalhes de conexão
- copie a string do campo "Conectar-se por meio do navegador ou localmente"
- Entre na sua VM
- cole a string de conexão ao banco de dados na VM e aperte enter, e entre com a senha criada. 
- no banco de dados logado, execute show databases; e terá o seguinte retorno:
```bash
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| teste_db           |
+--------------------+
5 rows in set (0.01 sec)
```
- note que o nome do banco de dados criado anteriormente vai ser listado, no meu caso foi "teste_db"
- Para testar a conexão, execute:
```
curl https://cdn3.gnarususercontent.com.br/2732-azure-cloud-criando-servidor-banco-dados-receber-aplicacao/config.json -o /tmp/config.json
```

- o comando acima vai gerar um config.json na pasta /tmp, sendo assim, será necessário editar este arquivo de acordo com as suas redenciais, como nome de login, o banco, hostname e senha.
- faça um gitclone neste repositorio: 
```
git clone https://github.com/alura-cursos/1862-sequelize/
```

e adicione o arquivo config.json modificado no seguinte diretório: /home/azureuser/1862-sequelize/api/config
- Prepare a VM para ser um web service e starte a aplicação
```
 npm install express --save
 npm install
 DEBUG=curso-alura:* npm start
```

- Libere a 3000, selecione sua VM e no menu lateral em Rede, selecione "Configuração de Rede", crie uma regra de porta de Entrada e Saída. 
- Na criação de regra, mude a porta 8080 para 3000 e clique em "Adicionar", faça o meso com Rega de Saída
- teste a conexão:
```
http://172.190.32.109:3000/turmas
```

- se retornar, deu tudo certo!: 
```
// 20241223103213
// http://172.190.32.109:3000/turmas

[
  {
    "id": 1,
    "data_inicio": "2021-10-17",
    "createdAt": "2021-10-17",
    "updatedAt": "2021-10-17",
    "nivel_id": 1,
    "docente_id": 1
  }
]
```