# Composer
## Instalando

Para instalar o composer devemos acessar o site official e baixar o instalador ou o arquivo composer.phar.

### Com o instalador

É só baixar o executável no <a href="https://getcomposer.org/download/">site oficial</a> e depois de instalar se certificar que a pasta do composer esta na variável path, exe: "C:\ProgramData\ComposerSetup\bin;".

### Sem instalador

Sem instalador podemos usar o arquivo composer.phar, podemos baixar ele no <a href="https://getcomposer.org/download/">site oficial</a> do composer.
Depois de baixar é so colocar dentro da pasta root do projecto.

## Como gerar o arquivo de para metrização (composer.json)

Usando a IDEA PHPStorm vá em tools e depois em composer e init composer após isso clique em using .phar agora selecione o interpretador PHP e ok.
Agora tens o arquivo composer.json

## Como parametrizar o ficheiro composer.json

### Campos de informação

#### name
 Aqui colocamos o nome (pode ser nickname como eacuamba para min) do desenvolvedor (ou empresa que desenvolveu) barra o nome do projecto, sempre separe por underscore. 
 
 Exemplo: <pre> "name" : "eacuamba/delivery_food" </pre>
 
#### description
 Aqui vamos colocar uma pequena descrição da importância do projecto.
 
 Exemplo: <pre> "description" : "Um aplicativo para gerir e entregas de comida, permitir o agendamento para entrega de comida." </pre>

#### minimum-stability
 Aqui vamos definir a estabilidade minima para poder-se usar o software em produção, podendo os valores serem "stable, alpha, beta, dev, rc, ..." entre outros.
 
 Exemplo: 
 <pre>"minimum-stability" : "stable" </pre>
 
#### licence
 Aqui vamos definir a licença do projecto, devemos ser muito cuidadosos ao escolher a licença, de preferência escolha proprietary se for um projecto para um cliente que será privado e no fim guarde no GITHUB como private e não public, caso o projecto seja público selecione MIT ou apache-2.0 e tem vários.
 
 Exemplo: 
 <pre> "licence" : "MIT" </pre>
 
#### authors
 Aqui vamos definir os autores dos projetos, podemos definir vários autores em um array de objeto [{},{}] JSON.
 
 Exemplo:
 <pre>
 "authors" : [
    {
        "name" : "Edilson Alexandre Cuamba",
        "email" : "edilsoncuamba@gmail.com",
        "role" : "Architect Software",
        "homepage" : "https://eacuamba.thundermozambique.com"
    }
 ],
 </pre>
 
### Vamos definir parâmetros de configuração do projeto
#### Campos

**config** - No config vamos definir alguns parametros para o composer.
 
 **vendor-dir** - Aqui vamos definir o directorio onde o composer vai instalar as dependencias que baxaremos do packgist.
  
 <pre>
    "config" : {
        "vendor-dir" : "vendor",
    },
 </pre>
 
 **autoload** - Vamos dizer ao composer que arquivos ele deverá carregar automaticamente, e depois ele vai gerar o arquivo de inclusão, assim com apenas um require("arquivo"), vamos ter todas as bibliotecas disponíveis para usar. 
 
  Para isso vamos usar a <a href="https://www.php-fig.org/">**PSR-4**</a> que é uma convenção usada para organização e uso de bibliotecas, dentro do <a href="https://www.php-fig.org/">**PSR-4**</a> vamos definir a fonte "source\\" que é o namespace da minha aplicação o fornecedor do projecto e passamos "source\" o directorio do carregamento. 
  
  Depois vamos definir o **files** que é para dizermos ao autoload para carregar arquivos especificos. Por exemplo no nosso caso estamos carregando o ficheiro source/Config.php para o arquivo autoload, assim ele sempre estará disponivel.
  
  <pre>
    "autoload" : {
        "psr-4" : {
            "source\\" : "source/"
        },
       "files" : [
            "source/Config.php"
        ]
    },
  </pre>
  
  **require** - No require vamos definir as bibliotecas que queremos biscar do packagist, para o nosso projecto.
  Por exemplo aí buscamos a biblioteca <a href="phpmailer/phpmailer">phpmailer/phpmailer</a> do packagist, esse nome podemos encontrar no proprio packagist não precisa decorrar.
  
  Como funciona as verões dos pacotes?
  No nosso pacote temos três valores **"`6.0.*`"** :
  
  O **`*`** indica a versão final, esta versão é retro compativel e não vai trazer problemas se for actulizada, por isso podemos buscar qualquer ou a mais recente e estavel.
  
  P **`0`** indica uma verão que pode causar problemas de copatibilidade, por isso está não se mexe com frequencia.
  
  O **`6`** indica a versão do projecto, aqui as mudanças são muito profunndas e podem mudar tudo, a arquitetura do projecto.
  <pre>
    "require" : {
        "phpmailer/phpmailer" : "6.0.*"
    }
  </pre>
  
## Como instalar as dependencias
Para instalar as dependencias podemos usar os comandos composer install e composer update, a diferença entre ele é que um o installer vai apensa instalar e o outro update vai instalar e actualizar os que estão desactualizados.

*Se for a primeira vez a rodares o composer use o update para ele gerar o arquivo .lock, esse compose.lock é o arquivo onde vamos encontrar as informações sobre a versão exata das bibliotecas que foram instaladas. Isso significa que assim que quando definimos a versão com `*` temos no composer.lock as informações exatas que foram instaladas e se quisermos instalar essas versões de forma exata devemos usa o `composer install` para instalar essa versões aí exatamente como estão aí.*

<pre>
    composer install
    ||
    composer update
</pre>

