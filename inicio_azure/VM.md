# Maquinas Virtuais (VM) no Azure
## Grupo de recursos
* Grupo de recursos, basicamente tudo que for feito, criação de máquinas, redes, subnets e etc vão ser armazenados no grupo de recursos.. ou seja, o grupo de recursos pode ser um encapsulamento dos recursos. Um container que junta todos os recursos para mais organização

- Pesquise por grupo de recursos
- Clique em criar
- Informe um nome para o seu grupo de recursos
- Deixe a região East US marcada
- Clique em Avançar

- Agora, em marcações, defina um nome e um valor, ex: (Nome: env - Valor: dev), Marcações são tags, para poder pesquisar por cobranças, filtros e etc.
- Clique em avançar, nesta tela vai ser a parte de revisão de tudo oque foi feito
- Com tudo ok, clique em Criar


## Criando uma VM
- No canto superior esquerdo, clique no icone de menu e depois em "Criar recurso"
- Clique em "Criar" em Máquina virtual

* Criação da VM
- no campo Assinatura, seleciona a sua assinatura
- no campo Grupo de recursos, selecione o grupo de recurso criado anteriormente

* Detalhes da instancia
- no campo Nome da máquina virtual, dê um nome para a sua VM
- no campo Região, selecione a mesma região do grupo de recurso East US
- no campo Opções de disponibilidade, selecione a opção "Nenhuma redundância infraestrutura necessária" (Marque essa opção se a sua assinatura for de estudante) As Opções de Disponibilidade definem como a máquina virtual será configurada para garantir maior proteção contra falhas. Elas podem distribuir VMs entre racks ou zonas diferentes para alta disponibilidade.
- no campo Tipo de segurança, deixe padrão
- no campo imagem, selecione ubuntu 22.04
- no campo Arquitetura de VM, selecione x64
- no campo Executar com desconto de Spot do Azure deixe desmarcado a caixinha
- no campo tamanho, selecione o tamanho desejado: Standard_D2s_v3 - 2 vcpus, 8 GiB memória (US$ 70,08/mês)
- no campo Tipo de Autenticação, selecione a chave pública de SSH
- no campo Nome de usuário, dê um nome para o usuário da máquina ou deixe padrão mesmo azureuser
- no campo Origem de chave SSH pública, seelecione "Gerar um novo par de chaves", deixe marcado a opção "Formato SSH RSA"
- no campo Nome do par de chaves, dê um nome para sua chave
- no campo Portas de entrada públicas, deixe marcado a opção Permitir portas selecionadas
- Clique em Avançar: Discos

* Discos
- no campo Tamanho do disco do SO, selecione um tamanho
- no campo Tipo de disco de SO, selecione o tipo se é o HD standard, SSD standard ou SSD premium
- no campo Excluir com VM, deixe marcado se você tem ciencia de que quando for excluir uma VM a o hd vai junto, se deixar desmarcado, o hd fica intacto e você consegue criar uma nova VM e utilizar o mesmo disco
- nos campos restantes deixe como está, e clique em Avançar: Rede

* Redes
- Neste caso, como é uma conta de estudante, na parte de Redes, deixe tudo padrão do jeito que está e marque apenas a opção: " Excluir o IP público e a NIC quando a VM for excluída "
- Clique em Avançar: Gerenciamento


* Gerenciamento
- Para fins de estudo, deixe tudo padrão e clique em Avançar: Monitoramento


* Monitoramento
- Para fins de estudo, deixe tudo padrão e clique em Avanlar: Avançado


* Avançado
- Para fins de estudo, deixe tudo padrão e clique em Avanlar: Marcas


* Marcas
- Adicione o mesmo nome e valor que foi adicionado em grupos de recurso (env - Valor: dev)
- clique em Avançar: Revisar + Criar


* Revisar + Criar
- Nessa etapa, vai mostrar tudo que já foi feito e o preço da máquina
- Clique em criar
- Baixe a chave privada para prosseguir na criação da VM
- Aguarde a criação da VM, você pode ver o procedimento na parte de notificação e após a criação, clique em "Ir para o recurso"

## Conectando via SSH na VM criada
- Vá no seu grupo de recurso criado, clique na VM criada. 
- Quando clicado na VM criada, vai aparecer informações sobre a VM
- Na sua máquina local, vá no mesmo diretório que se encontra sua chave e digite:
```bash
ssh -i <nomedachaveprivada> usuario@ip-publico
```
- Atualize a máquina:
```
sudo apt-get update
sudo apt-get upgrade
```
