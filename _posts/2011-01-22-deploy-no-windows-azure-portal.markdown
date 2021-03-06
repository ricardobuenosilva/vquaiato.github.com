--- 
layout: post
title: "Deploy no Windows Azure: portal"
wordpress_id: 2900
wordpress_url: http://viniciusquaiato.com/blog/?p=2900
categories: 
- title: Windows Azure
  slug: windows-azure
  autoslug: windows-azure
tags: 
- title: Windows Azure
  slug: windows-azure
  autoslug: windows-azure
---
Fala galera, vamos falar mais um pouco de [Windows Azure](http://viniciusquaiato.com/blog/category/windows-azure/) (na boa a plataforma é muito legal).Para quem tem acompanhado estou organizando o MVC Summit, um evento totalmente focado em ASP.NET MVC. O que isso tem a ver com Azure? Simples: decidi migrar o site do Moca Host para o Azure.Neste post vou mostrar os passos necessários para realizar o deploy de uma aplicação no Windows Azure através do portal.

## Gerando o pacote do serviço Windows Azure no Visual Studio


O site do MVC Summit por enquanto é bem simples. É um site ASP.NET MVC 3 mas com conteúdo estático, ou seja, não estamos fazendo uso de banco de dados nem nada do tipo, é simples mesmo.Desta forma o que precisamos fazer é realizar o empacotamento do serviço como vemos abaixo.[![Gerando pacote deploy Windows Azure no VS2010](http://viniciusquaiato.com/images_posts/Gerando-pacote-Visual-Studio-300x177.png "Gerando pacote deploy Windows Azure no VS2010")](http://viniciusquaiato.com/images_posts/Gerando-pacote-Visual-Studio.png)



Após clicar em _publish_ veremos a seguinte tela. Basta escolhermos a primeira opção e darmos ok.[![Gerando pacote deploy Windows Azure V2010 2](http://viniciusquaiato.com/images_posts/Gerando-pacote-Visual-Studio-2-300x282.png "Gerando pacote deploy Windows Azure V2010 2")](http://viniciusquaiato.com/images_posts/Gerando-pacote-Visual-Studio-2.png)



Feito isso serão gerados 2 arquivos: um pacote e um de configurção(definição do serviço).Precisamos enviar nosso pacote e o arquivo de configuração/definição para o portal do Windows Azure.[![Pacote deploy Windows Azure gerado pelo VS2010](http://viniciusquaiato.com/images_posts/Pacote-deploy-Windows-Azure-gerado-300x210.png "Pacote deploy Windows Azure gerado pelo VS2010")](http://viniciusquaiato.com/images_posts/Pacote-deploy-Windows-Azure-gerado.png)



## Criando um Hosted Service no portal do Windows Azure
Criar um hosted service é um processo bastante simples, e a interface do portal está muito, mas muito simples de usar. É agradável e intuitiva.(Para acessar o portal é preciso ter criado uma conta do Windows Azure)Após acessarmos o portal([http://windows.azure.com](http://windows.azure.com)) precisamos seguir os passos abaixo:1. Acesar a área "Hosted Services, Storage Accounts & CDN"
2. Acesar "Hosted Services"
3. Clicar em "New Hosted Sservice"


[![Criando hosted Service Windows Azure Portal](http://viniciusquaiato.com/images_posts/Criando-hosted-Service-Windows-Azure-Portal-300x179.png "Criando hosted Service Windows Azure Portal")](http://viniciusquaiato.com/images_posts/Criando-hosted-Service-Windows-Azure-Portal.png)



Agora precisamos dar um nome e um endereço para nosso serviço, só para demonstrar criei um serviço com nome fictício:[![Criando hosted Service Windows Azure Portal 2](http://viniciusquaiato.com/images_posts/Criando-hosted-Service-Windows-Azure-Portal-2-300x179.png "Criando hosted Service Windows Azure Portal 2")](http://viniciusquaiato.com/images_posts/Criando-hosted-Service-Windows-Azure-Portal-2.png)



Vamos optar por não realizar um deploy no momento da criação do serviço, desta forma entendemos melhor como funciona cada uma das partes do processo.Após a criação do serviço o mesmo aparecerá na listagem de hosted services:[![Criando hosted Service Windows Azure Portal 3](http://viniciusquaiato.com/images_posts/Criando-hosted-Service-Windows-Azure-Portal-3-300x179.png "Criando hosted Service Windows Azure Portal 3")](http://viniciusquaiato.com/images_posts/Criando-hosted-Service-Windows-Azure-Portal-3.png)



## Criando um deploy no Azure Portal


Para criar um deploy precisamos primeiramente passar pelo staging. Staging pode ser compreendido como um servidor de homologação. Ele vai realizar o deploy do nosso serviço(web roles) exatamente como se fosse produção mas nos fornecerá uma url de acesso "temporária".Vamos então criar um "New Staging Deployment". [![Criando staging deployment windows azure portal](http://viniciusquaiato.com/images_posts/Criando-staging-deployment-windows-azure-portal.png "Criando staging deployment windows azure portal")](http://viniciusquaiato.com/images_posts/Criando-staging-deployment-windows-azure-portal.png)



Uma janela solicitando um nome, o arquivo de pacote e o arquivo de definição do serviço será apresentada:[![Criando deploy windows azure portal](http://viniciusquaiato.com/images_posts/Criando-deploy-windows-azure-portal-294x300.png "Criando deploy windows azure portal")](http://viniciusquaiato.com/images_posts/Criando-deploy-windows-azure-portal.png)



Você pode dar o nome que quiser para o seu deploy(eu sugiro que seja um nome que signifique algo, por exemplo 'deploy alterações do menu 22/01/2010').Os arquivos foram gerados pelo Visual Studio nos passos anteriores.Nosso serviço então será enviado para o Windows Azure e inicializado, ficando no Staging.[![Criando deploy windows azure portal upload](http://viniciusquaiato.com/images_posts/Criando-deploy-windows-azure-portal-upload-300x68.png "Criando deploy windows azure portal upload")](http://viniciusquaiato.com/images_posts/Criando-deploy-windows-azure-portal-upload.png)



[![Criando deploy windows azure portal inicializacao](http://viniciusquaiato.com/images_posts/Criando-deploy-windows-azure-portal-inicializacao-300x30.png "Criando deploy windows azure portal inicializacao")](http://viniciusquaiato.com/images_posts/Criando-deploy-windows-azure-portal-inicializacao.png)



[![Criando deploy windows azure portal ready](http://viniciusquaiato.com/images_posts/Criando-deploy-windows-azure-portal-ready-300x82.png "Criando deploy windows azure portal ready")](http://viniciusquaiato.com/images_posts/Criando-deploy-windows-azure-portal-ready.png)



## Promovendo o deploy para produção no Azure Portal


Após testarmos e verificarmos que a aplicação está ok no ambiente de staging vamos promover esta aplicação para produção.O que acontece aqui é muito bacana. Promover uma aplicação para produção do Azure faz uso do Swap VIP ou troca de IP Virtual. Isso quer dizer que nossa app que estava em staging vai continuar na máquina de staging porém essa máquina de staging vai se tornar a máquina de produção. Ou seja, exatamente o ambiente em que a app foi homologada é que vai se tornar produção evitando assim quaisquer riscos de mover a aplicação para outro servidor.Para realizarmos essa troca de staging para produção basta clicarmos em Swap VIP no menu superior do portal:[![Swap VIP Windows Azure portal](http://viniciusquaiato.com/images_posts/Swap-VIP-300x63.png "Swap VIP Windows Azure portal")](http://viniciusquaiato.com/images_posts/Swap-VIP.png)



Precisamos confirmar a operação:[![Swap VIP Windows Azure portal confirmacao](http://viniciusquaiato.com/images_posts/Swap-VIP-confirmacao-300x172.png "Swap VIP Windows Azure portal confirmacao")](http://viniciusquaiato.com/images_posts/Swap-VIP-confirmacao.png)



Após o Swap VIP finalizar teremos nosso deploy que esta como staging sendo o atual production, e o que era production sendo o atual staging:[![Swap VIP Windows Azure portal finalizado](http://viniciusquaiato.com/images_posts/Swap-VIP-finalizado-300x104.png "Swap VIP Windows Azure portal finalizado")](http://viniciusquaiato.com/images_posts/Swap-VIP-finalizado.png)



## Apagando o servidor de staging no Azure Portal


Quando promovemos um deploy de staging para produção, o que tínhamos antes em produção vira nossa máquina de staging, ou seja, o Windows Azure continua alocando essa máquina para nós. Isto quer dizer que estamos sendo cobrados por isso.Para evitar que sejamos cobrados pela máquina de staging precisamos parar o serviço e então deletar esta máquina.[![Parando e excluindo instancia role Windows Azure portal](http://viniciusquaiato.com/images_posts/Parando-role-300x66.png "Parando e excluindo instancia role Windows Azure portal")](http://viniciusquaiato.com/images_posts/Parando-role.png)

É recomendado que você mantenha a máquina de staging pelo tempo suficiente que precisar para ter certeza de que tudo que está em produção está ok. Caso este custo não seja um problema para você, mantenha o staging (para mim é um problema pois o evento não possui financiadores :P).

## Resumo
O deploy de uma aplicação no Windows Azure é algo bastante simples. Tudo que precisamos é gerar um pacote e subir dois arquivos no portal do Azure. Sem malabarismos, sem truques secretos.Veremos em um próximo post como fazer isso diretamente do Visual Studio 2010, sem a necessidade de abrir o portal, deixando a tarefa um pouco mais simples. E futuramente como fazer isso de forma automatizada em um script de build por exemplos.Até lá acompanhem o [post do Lucas Romão](http://azureservicesbr.ning.com/profiles/blogs/publicando-sua-app-no-azure)(que está com a interface antiga do portal do Windows Azure mas ajuda bastante).

Abraços,
Vinicius Quaiato.
