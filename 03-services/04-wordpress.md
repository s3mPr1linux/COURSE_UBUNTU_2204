#Autor: Robson Vaamonde<br>
#Procedimentos em TI: http://procedimentosemti.com.br<br>
#Bora para Prática: http://boraparapratica.com.br<br>
#Robson Vaamonde: http://vaamonde.com.br<br>
#Facebook Procedimentos em TI: https://www.facebook.com/ProcedimentosEmTi<br>
#Facebook Bora para Prática: https://www.facebook.com/BoraParaPratica<br>
#Instagram Procedimentos em TI: https://www.instagram.com/procedimentoem<br>
#YouTUBE Bora Para Prática: https://www.youtube.com/boraparapratica<br>
#Data de criação: 16/01/2023<br>
#Data de atualização: 12/12/2023<br>
#Versão: 0.12<br>

OBSERVAÇÃO IMPORTANTE: COMENTAR NO VÍDEO DO WORDPRESS SE VOCÊ CONSEGUIU FAZER O DESAFIO COM 
A SEGUINTE FRASE: Desafio do WordPress realizado com sucesso!!! #BoraParaPrática

COMPARTILHAR O SELO DO DESAFIO NAS SUAS REDES SOCIAIS (LINKEDIN, FACEBOOK, INSTRAGRAM)
MARCANDO: ROBSON VAAMONDE COM AS HASHTAGS E COPIANDO O CONTEÚDO DO DESAFIO ABAIXO: 

LINK DO SELO: https://github.com/vaamonde/ubuntu-2204/blob/main/selos/04-wordpress.png

#boraparapratica #boraparaprática #vaamonde #robsonvaamonde #procedimentosemti #ubuntuserver 
#ubuntuserver2204 #desafiovaamonde #desafioboraparapratica #desafiowordpress #desafiocms

Conteúdo estudado nesse desafio:<br>
#01_ Instalado as Dependências do WordPress;<br>
#02_ Criando a Base de Dados e Usuário no MySQL Server;<br>
#03_ Baixando o WordPress do Site Oficial;<br>
#04_ Descompactando e Movendo o conteúdo do Site para o Apache2;<br>
#05_ Alterando as Permissões de Arquivos e Diretórios do WordPress;<br>
#06_ Configurando o Arquivo WP-CONFIG.PHP do WordPress;<br>
#07_ Habilitado os Módulos do Apache2;<br>
#08_ Acessando o WordPress e fazendo sua Pré-Configuração;<br>
#09_ Desafio de Postagem, Temas e Plugins do CMS WordPress.

Site Oficial do Apache2: https://httpd.apache.org/<br>
Site Oficial do PHP (7.x ou 8.x): https://www.php.net/<br>
Site Oficial do MySQL: https://www.mysql.com/<br>
Site Oficial do WordPress: https://br.wordpress.org/

Site Oficial do W3C School HTML5: https://www.w3schools.com/html/default.asp<br>
Site Oficial do W3C School CSS: https://www.w3schools.com/css/default.asp<br>
Site Oficial do W3C School JavaScript: https://www.w3schools.com/js/default.asp<br>
Site Oficial do W3C School PHP: https://www.w3schools.com/php/default.asp

WordPress é um sistema livre e aberto de gestão de conteúdo para internet, baseado em PHP<br>
com banco de dados MySQL, executado em um servidor interpretador, voltado principalmente<br>
para a criação de páginas eletrônicas e blogs online.

[![WordPress](http://img.youtube.com/vi/J6xVAocGyZg/0.jpg)](https://www.youtube.com/watch?v=J6xVAocGyZg "WordPress")

Link da vídeo aula: https://www.youtube.com/watch?v=J6xVAocGyZg

#01_ Instalando as Dependências do WordPress<br>

	#atualizando as listas do Apt
	sudo apt update
	
	#instalando as dependências do WordPress
	#opção da contra barra (\): criar uma quebra de linha no terminal
	sudo apt install php8.1-bcmath php8.1-mbstring  php8.1-dev php8.1-curl php8.1-mysql \
	php8.1-xml php8.1-zip php8.1-soap php8.1-imagick php8.1-intl php-json php-pear unzip \
	pwgen libmcrypt-dev ghostscript libapache2-mod-php zlib1g zlib1g-dev

#02_ Criando a Base de Dados do WordPress no MySQL Server<br>

	#opções do comando mysql: -u (user), -p (password)
	sudo mysql -u root -p

	#criando a Base de Dados do WordPress
	CREATE DATABASE wordpress;

	#criando o usuário ba Base de Dados do WordPress
	CREATE USER 'wordpress' IDENTIFIED WITH mysql_native_password BY 'wordpress';
	
	#aplicando as permissões do usuário WordPress
	GRANT USAGE ON *.* TO 'wordpress';
	GRANT ALL PRIVILEGES ON wordpress.* TO 'wordpress';
	FLUSH PRIVILEGES;
	exit

	#opções do comando mysql: -u (user), -p (password)
	sudo mysql -u wordpress -p

	#visualizando a base de dados do WordPress
	SHOW DATABASES;
	USE wordpress;
	exit

#03_ Fazendo o download do WordPress e descompactando o seu conteúdo no diretório padrão do Apache2 Server<br>

	#acessando diretório temporário
	cd /tmp

	#fazendo o download do WordPress do site Oficial do Brasil
	#opção do comando wget: -O (output-document)
	wget -O wordpress.zip https://br.wordpress.org/latest-pt_BR.zip

	#descompactando o arquivo do WordPress
	unzip wordpress.zip

	#movendo o conteúdo do WordPress para o diretório do Apache2 Server
	#opção do comando mv: -v (verbose)
	sudo mv -v wordpress/ /var/www/html/wp/

	#alterando as permissões dos diretórios e arquivos do WordPress
	#opção do comando chown: -R (recursive), -f (silent), -v (verbose), www-data (user), www-data (group)
	#opção do comando find: . (path), -type d (directory), , type f (file), -exec (execute command)
	#opção do comando chmod: -v (verbose), 755 (Dono=RWX,Grupo=R-X,Outros=R-X)
	#opção do comando chmod: -v (verbose), 644 (Dono=RW-,Grupo=R--,Outros=R--)
	#opção do comando {} \;: executa comandos em lote e aplicar as permissões para cada arquivo/diretório em loop
	sudo chown -Rfv www-data.www-data /var/www/html/wp/
	sudo find /var/www/html/wp/. -type d -exec chmod -v 755 {} \;
	sudo find /var/www/html/wp/. -type f -exec chmod -v 644 {} \;

#04_ Editando o arquivo de conexão com o Banco de Dados e Salt do WordPress<br>

	#acessando o diretório do WordPress
	cd /var/www/html/wp/

	#criando o arquivo de configuração do banco de dados do WordPress
	#opção do comando cp: -v (verbose)
	sudo cp -v wp-config-sample.php wp-config.php

	#editando o arquivo de configuração do WordPress
	sudo vim wp-config.php
	INSERT

		#alterar os valores das variáveis "define" a partir da linha 23
		
		#variável do nome do banco de dados
		define( 'DB_NAME', 'wordpress' );
		
		#variável do nome do usuário de autenticação do banco de dados
		define( 'DB_USER', 'wordpress' );
		
		#variável da senha do usuário do banco de dados
		define( 'DB_PASSWORD', 'wordpress' );
	
		#configuração do Salt do WordPress site: https://api.wordpress.org/secret-key/1.1/salt/
		#mais informações sobre o Salt's do WordPress: https://www.hostinger.com.br/tutoriais/wordpress-salt
		#copiar o conteúdo do Salt e colocar a partir da linha: 53
		#OBSERVAÇÃO IMPORTANTE: remover as linhas existentes antes de copiar/colar as
		#novas linhas do Salt, utilizar a opção: dd do Editor de Texto VIM. 

	#sair e salvar o arquivo
	ESC SHIFT :x <Enter>

#05_ Habilitando os módulos do Apache2 Server utilizados pelo WordPress<br>

	#habilitar os módulos do Apache2 Server
	sudo a2enmod cgi alias authz_host deflate dir expires headers mime rewrite autoindex negotiation setenvif

	#reiniciar o serviço do Apache2 Server
	sudo systemctl restart apache2
	sudo systemctl status apache2

#06_ Acessando e configurando o WordPress no navegador<br>

	firefox ou google chrome: http://endereço_ipv4_ubuntuserver/wp

	#Informações que serão solicitadas na configuração via Web do WordPress
	Português do Brasil: Continuar;
	Informação necessária
		Título do site: Seu Nome e Sobrenome;
		Nome de usuário: admin;
		Senha: pti@2018;
		Confirme a senha: On (Habilitado) Confirmar o uso de uma senha fraca;
		O seu e-mail: admin@ptin.intra; 
	<Instalar WordPress>
	<Acessar>

	#Tela de login do WordPress
	firefox ou google chrome: http://endereço_ipv4_ubuntuserver/wp/wp-login.php
		Nome de usuário ou endereço de email: admin
		Senha: pti@2018
		Lembrar-me: On (Habilitado)
		<Acessar>
	
	#Configuração dos Links Permanentes do WordPress
	Configurações
		Links permanentes
			Configurações de Links Permanentes
				Configurações Comuns
					Estrutura de Links Permanentes
						ON (Selecionar): Padrão (http://172.16.1.20/wp/?=123)
		<Salvar Alterações>

	#Tela do site do WordPress
	firefox ou google chrome: http://endereço_ipv4_ubuntuserver/wp/

#07_ DESAFIO-01: FAZER A INSTALAÇÃO DE UM NOVO TEMA DO WORDPRESS, FAZER A CRIAÇÃO DE 02 (DUAS)
POSTAGEM NO WORDPRESS DE QUALQUER CONTEÚDO ADICIONANDO PELO MENOS UMA IMAGEM.

#08_ DESAFIO-02: FAZER A INSTALAÇÃO E CONFIGURAÇÃO DE 02 (DOIS) PLUGINS DO WORDPRESS MAIS USADO
NO DIA A DIA: Wordfence Security E W3 Total Cache.

#09_ DESAFIO-03: NO TEMA QUE VOCÊ INSTALOU, VERIFICAR A POSSIBILIDADE DE ADICIONAR OS ÍCONES DO
GITHUB, LINKEDIN E FACEBOOK, ADICIONAR TAMBÉM OS LINKS PARA O SITE CRIADO NO DESAFIO DO APACHE2,
FACILITANDO O ACESSO A SUAS PÁGINAS CRIADAS EM HTML E PHP.

=========================================================================================

OBSERVAÇÃO IMPORTANTE: COMENTAR NO VÍDEO DO WORDPRESS SE VOCÊ CONSEGUIU FAZER O DESAFIO COM 
A SEGUINTE FRASE: Desafio do WordPress realizado com sucesso!!! #BoraParaPrática

COMPARTILHAR O SELO DO DESAFIO NAS SUAS REDES SOCIAIS (LINKEDIN, FACEBOOK, INSTRAGRAM)
MARCANDO: ROBSON VAAMONDE COM AS HASHTAGS E COPIANDO O CONTEÚDO DO DESAFIO ABAIXO: 

LINK DO SELO: https://github.com/vaamonde/ubuntu-2204/blob/main/selos/04-wordpress.png

#boraparapratica #boraparaprática #vaamonde #robsonvaamonde #procedimentosemti #ubuntuserver 
#ubuntuserver2204 #desafiovaamonde #desafioboraparapratica #desafiowordpress #desafiocms