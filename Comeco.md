# Começando na Azure, utiliznado o básico. 
- No diretório incio_azure, Tem os seguintes readme.d: VM, MySQL, AzureVirtualNetwor

## VM.md
- Neste readme, assim como os demais, tem como objetivo de passos na criação de uma VM na Azure, pois estou começando a estudar cloud e optei pela Azure. Então, neste readme de VM eu citei alguns passos de criação de um grupo de recursos e criação de uma VM para quem nunca criou um grupo de recursos e uma VM e também para fixar os conhecimento da criação, pois a única maneira que eu consigo aprender de verdade, é anotando e praticando.

## MySQL
- Aqui, criei um recurso da azure de banco de dados do mysql. Usei um próprio banco de dados da Azure, e contectei minha aplicação neste recurso.

## AzureVirtualNetwork.md
- Aqui, aprendi a criar uma subnet, criei uma outra VM para ser o frontend e criei uma subnet associada a essa vm frontend, essa subnet está "vinculada" a vnet do backend, sendo assim não ter conflitos de portas e configurei o acesso ao backend apenas da VM frontend, sem a necessidade de acessar o backend pelo navegador