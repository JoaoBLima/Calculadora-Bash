
# Calculadora Simples em Bash e CGI

Este projeto é uma calculadora simples desenvolvida em Bash e CGI, que permite ao usuário inserir dois números e escolher uma operação (adição, subtração, multiplicação ou divisão). O resultado da operação é exibido em uma página HTML gerada dinamicamente.

## Pré-requisitos

- **Servidor Web com suporte a CGI**: O projeto foi testado usando o servidor Apache com o módulo `cgi-bin` habilitado.
- **Sistema Operacional**: Linux Ubuntu.
- 
## Estrutura do Projeto

- **calculadora.html**: Página HTML com o formulário para o usuário inserir os números e escolher a operação.
- **calculadora.cgi**: cript Bash que processa os dados do formulário e retorna o resultado.

# Configuração de CGI no Ubuntu com Apache

Este guia explica como configurar o **Common Gateway Interface (CGI)** no Ubuntu, usando o servidor web **Apache**. O CGI permite a execução de scripts no servidor para gerar conteúdo dinâmico em resposta a solicitações de clientes.

## Pré-requisitos

- Ubuntu com privilégios de superusuário (root ou sudo).
- Apache instalado.

## Passo a Passo para Configuração

### 1. Instalar o Apache

Se o Apache ainda não estiver instalado, execute os comandos abaixo:

```bash
sudo apt update
sudo apt install apache2
```

### 2. Habilitar o Módulo CGI no Apache

Para que o Apache suporte scripts CGI, é necessário habilitar o módulo `mod_cgi`:

```bash
sudo a2enmod cgi
```

Em seguida, reinicie o Apache para aplicar as alterações:

```bash
sudo systemctl restart apache2
```

### 3. Configurar o Diretório para Scripts CGI

Por padrão, o Apache usa o diretório `/usr/lib/cgi-bin/` para scripts CGI. Edite o arquivo de configuração do Apache para garantir que este diretório esteja configurado corretamente:

```bash
sudo nano /etc/apache2/sites-available/000-default.conf
```

No arquivo, adicione a linha abaixo dentro do bloco `<VirtualHost>`:

```apache
ScriptAlias /cgi-bin/ /usr/lib/cgi-bin/
```

### 4. Permitir Execução de CGI no Diretório

Ainda no arquivo de configuração, defina as permissões para que o Apache possa executar scripts CGI dentro do diretório:

```apache
<Directory "/usr/lib/cgi-bin">
    Options +ExecCGI
    AddHandler cgi-script .cgi .pl .sh
    Require all granted
</Directory>
```
### 5. Mover os Arquivos para os Diretórios Corretos
sudo mv calculadora.html /var/www/html/

sudo mv calculadora.cgi /usr/lib/cgi-bin/

### 6. Tornar o Script Executável

Dê permissão de execução ao script criado:

```bash
sudo chmod +x /usr/lib/cgi-bin/calculadora.cgi
```

### 7. Reiniciar o Apache

Para aplicar todas as configurações, reinicie o Apache:

```bash
sudo systemctl restart apache2
```

### 8. Executar o Script CGI

```
sudo /usr/lib/cgi-bin/calculadora.cgi

```


### 9. Verificar Logs de Erro (Opcional)

Se o script não funcionar como esperado, consulte o log de erros do Apache para mais informações:

```bash
sudo tail -f /var/log/apache2/error.log
```

### 10. Executar o calculadora.html
Abra o navegador e acesse a página HTML:
http://localhost/calculadroa.html

### 11. Vídeo do projeto funcionado
https://drive.google.com/file/d/1DfdqYPvsWv_0Pp3BNCQHdpd_UMrE1Xgs/view?usp=sharing
## Conclusão

Com estas etapas, você configurou o ambiente CGI no Ubuntu com Apache. Agora é possível executar scripts no servidor e gerar conteúdo dinâmico em resposta a interações do cliente. Para adicionar mais funcionalidades, crie scripts em linguagens como Shell, Perl ou Python e armazene-os no diretório CGI configurado.

