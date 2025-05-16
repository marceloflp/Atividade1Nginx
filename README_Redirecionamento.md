# Configuração de Servidor Nginx para a Aplicação 'Cafeteria'

**A APLICAÇÃO UTILIZADA AQUI ESTÁ NO REPOSITÓRIO https://github.com/marceloflp/cafeteria-web. Clone ele para seguir ou faça outra do zero se assim preferir.**

1- Uma aplicação foi criada no diretório '/var/www/' chamado 'cafeteria'. Nesse caso, o caminho para o diretório é: /var/www/cafeteria

1.2- No diretório da aplicação, rode o seguinte comando para poder preparar a aplicação para produção: 
npm run build

1.3- Após isso, a pasta dist será criada. É graças a ela que aplicação será rodada no nginx.


PS: Se os diretórios "/etc/nginx/sites-available" e "/etc/nginx/sites-enabled" não existirem em sua máquina, rode o seguinte comando para criá-los antes de executar o passo dois:
sudo mkdir -p /etc/nginx/sites-available
sudo mkdir -p /etc/nginx/sites-enabled

2- Um arquivo chamado 'aplicacao.conf' foi criado no diretório /etc/nginx/sites-available/aplicacao. Nesse arquivo, informações devem ser adicionadas para configurar o servidor nginx. Para isso, o arquivo é aberto no terminal com o seguinte comando:
sudo nano /etc/nginx/sites-available/aplicacao.conf

2.1 Após isso, as seguintes informações são adicionadas:
          
server {
        listen 80;
        listen [::]:80;

        server_name localhost; #Nome do servidor
        root /var/www/cafeteria/dist; #Caminho para a pasta 'dist'
        index index.html index.htm;
        location / {
                try_files $uri $uri/ /index.html; #Tenta encontrar o arquivo solicitado, mas se não encontrar, redireciona para index.html
        }
}

Salve e feche o terminal.

2.2- Crie um link simbólico no diretório ''/etc/nginx/sites-enabled/'' para habilitar a aplicação configurada em 'sites-avaliable/' com o seguinte comando':
sudo ln -s /etc/nginx/sites-available/aplicacao.conf /etc/nginx/sites-enabled/

3- Em seguida, rode o seguinte comando para verificar se há algum erro no servidor:
sudo nginx -t

3.1 Verifque se há algum erro e corrija. Se não houver, siga o próximo passo.


4- Agora, reinicie o servidor nginx com o seguinte comando:
sudo systemctl restart nginx


5- Digite ''localhost'' na abrra de pesquisa do navegador e confira se a aplicação está funcionando.
