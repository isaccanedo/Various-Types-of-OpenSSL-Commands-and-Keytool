# Various-Types-of-OpenSSL-Commands-and-Keytool
:key: # Various Types of OpenSSL Commands and Keytool

## Comandos OpenSSL e lista de keytool SSL
OpenSSL é uma implementação de código aberto de protocolos SSL/TLS e é considerada uma das ferramentas SSL mais versáteis. É uma biblioteca escrita em linguagem de programação C que implementa as funções criptográficas básicas. OpenSSL tem versões diferentes para a maioria dos sistemas operacionais semelhantes ao Unix, que incluem Mac OC X, Linux e Microsoft Windows etc.

O SSL aberto é normalmente usado para gerar uma solicitação de assinatura de certificado (CSR) e uma chave privada para diferentes plataformas. No entanto, ele também possui várias funções diferentes, que podem ser listadas a seguir. É usado para:

- Ver detalhes sobre um CSR ou certificado
- Compare o hash MD5 de um certificado e uma chave privada para garantir que eles correspondam
- Verifique a instalação adequada do certificado em um site
- Converta o formato do certificado

A maioria das funções mencionadas abaixo também pode ser executada sem envolver o OpenSSL usando essas ferramentas SSL convenientes. Aqui, reunimos alguns dos comandos OpenSSL mais comuns.

## Comandos OpenSSL gerais
Estes são o conjunto de comandos que permitem aos usuários gerar CSRs, certificados, chaves privadas e muitas outras tarefas diversas. Aqui, listamos alguns desses comandos:

### (1) Gerar uma solicitação de assinatura de certificado (CSR) e uma nova chave privada

```
openssl req -out CSR.csr -new -newkey rsa:2048 -nodes -keyout privateKey.key
```

### (2) Gerar um certificado autoassinado

```
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout privateKey.key -out certificate.crt
```

### (3) Criar CSR com base em uma chave privada existente

```
openssl req -out CSR.csr -key privateKey.key –new
```

### (4) Criar CSR com base em um certificado existente

```
openssl x509 -x509toreq -in certificate.crt -out CSR.csr -signkey privateKey.key
```

### (5) Remoção de senha de uma chave privada

```
openssl rsa -in privateKey.pem -out newPrivateKey.pem
```

## Comandos de verificação SSL
Esses comandos são muito úteis se o usuário deseja verificar as informações em um certificado SSL, uma chave privada e CSR. Poucas ferramentas online também podem ajudá-lo a verificar CSRs e certificados SSL.

### (1) Solicitação de assinatura de certificado (CSR)
```
openssl req -text -noout -verify -in CSR.csr
```

### (2) Chave Privada

```
openssl rsa -in privateKey.key –check
```

### (3) Certificado SSL

```
openssl x509 -in certificate.crt -text –noout
```

### (4) Arquivo PKCS # 12 (.pfx ou .p12)

```
openssl pkcs12 -info -in keyStore.p12
```

## Comandos de conversão
De acordo com o título, esses comandos ajudam a converter os certificados e as chaves em diferentes formatos para dar-lhes compatibilidade com tipos de servidores específicos. Por exemplo, um arquivo PEM, compatível com o servidor Apache, pode ser convertido para PFX (PKCS # 12), após o que seria possível trabalhar com Tomcat ou IIS. No entanto, você também pode usar o Conversor SSL para alterar o formato, sem ter que envolver OpenSSL.

### (1) Converter arquivos DER (.crt, .cer, .der) para PEM

```
openssl x509 -(2) Converter PEM em DERinform der -in certificate.cer -out certificate.pem
```

### (2) Converter PEM em DER

```
openssl x509 -outform der -in certificate.pem -out certificate.der
```

### (3) Converter arquivo PKCS # 12 (.pfx, .p12) contendo uma chave privada e certificado para PEM

```
openssl pkcs12 -in keyStore.pfx -out keyStore.pem –nodes
```

Para produzir apenas a chave privada, os usuários podem adicionar –nocerts ou –nokeys para produzir apenas os certificados.

### (4) Converter o certificado PEM (arquivo e uma chave privada) para PKCS # 12 (.pfx # 12)

```
openssl pkcs12 -export -out certificate.pfx -inkey privateKey.key -in certificate.crt -certfile CACert.crt
```

## Depuração usando comandos OpenSSL
Se houver mensagens de erro surgindo sobre a sua chave privada não corresponder ao certificado ou que o certificado recém-instalado não é confiável, você pode contar com um dos comentários mencionados abaixo. Você também pode usar a ferramenta de verificação de certificado SSL para verificar a instalação correta de um certificado SSL.

### (1) Verifique a conexão SSL (todos os certificados, incluindo intermediários, devem ser exibidos)

Aqui, todos os certificados devem ser exibidos, incluindo também os intermediários.

```
openssl s_client -connect www.paypal.com:443
```

### (2) Verifique o hash MD5 da chave pública

Isso é para garantir que a chave pública corresponda ao CSR ou à chave privada.

```
openssl x509 -noout -modulus -in certificate.crt | openssl md5
openssl rsa -noout -modulus -in privateKey.key | openssl md5
openssl req -noout -modulus -in CSR.csr | openssl md5
```

## Lista SSL Keytool
Java Keytool é um utilitário de gerenciamento de chave e certificado que permite aos usuários armazenar em cache o certificado e gerenciar seus próprios pares de chaves e certificados públicos ou privados. Java Keytool armazena todas as chaves e certificados em um ‘Keystore’, que é, por padrão, implementado como um arquivo. Ele contém chaves privadas e certificados essenciais para estabelecer a confiabilidade do certificado principal e completar uma cadeia de confiança.

Cada certificado no Java Keystore tem um pseudônimo / alias exclusivo. Para criar um ‘Java Keystore’, você precisa primeiro criar o arquivo .jks contendo apenas a chave privada no início. Depois disso, você precisa gerar uma solicitação de assinatura de certificado (CSR) e gerar um certificado a partir dele. Depois disso, importe o certificado para o Keystore incluindo quaisquer certificados raiz.

O ‘Java Keytool’ basicamente contém várias outras funções que ajudam os usuários a exportar um certificado ou a visualizar os detalhes do certificado ou a lista de certificados no Keystore.

Aqui estão alguns comandos Java Keytool importantes:

## Para criar e importar
Esses comandos Keytool permitem aos usuários criar um novo Java Keytool keysKeystore, gerar uma solicitação de assinatura de certificado (CSR) e importar certificados. Antes de importar o certificado primário para o seu domínio, você precisa primeiro importar todos os certificados raiz ou intermediários.

## (1) Importar um certificado CA raiz ou intermediário para um keystore Java existente

```
keytool -import -trustcacerts -alias root -file Thawte.crt -keystore keystore.jks
```

### (2) Importar um certificado primário assinado para um keystore Java existente

```
keytool -import -trustcacerts -alias mydomain -file mydomain.crt -keystore keystore.jks
```

### (3) Gerar um keystore e certificado autoassinado

```
keytool -genkey -keyalg RSA -alias selfsigned -keystore keystore.jks -storepass password -validity 360 -keysize 2048
```

### (4) Gerar par de chaves e armazenamento de chaves Java

```
keytool -genkey -alias mydomain -keyalg RSA -keystore keystore.jks -keysize 2048
```

### (5) Gerar CSR para Java Keystore existente

```
keytool -certreq -alias mydomain -keystore keystore.jks -file mydomain.csr
```

## Para verificar
Os usuários podem verificar as informações em um certificado ou keystore Java usando os seguintes comandos:

### (1) Verifique um certificado individual

```
keytool -printcert -v -file mydomain.crt
```

### (2) Verifique os certificados no armazenamento de chaves Java

```
keytool -list -v -keystore keystore.jks
```

### (3) Verifique a entrada de armazenamento de chaves específica usando um alias

```
keytool -list -v -keystore keystore.jks -alias mydomain
```

## Outros comandos Java Keytool
### (1) Excluir um certificado do armazenamento de chaves Java Keystore

```
keytool -delete -alias mydomain -keystore keystore.jks
```

### (2) Alterar a senha no Java keystore / Alterar uma senha do Java keystore

```
keytool -storepasswd -new new_storepass -keystore keystore.jks
```

### (3) Exportar certificado do armazenamento de chaves Java

```
keytool -export -alias mydomain -file mydomain.crt -keystore keystore.jks
```

### (4) Liste o certificado CA confiável

```
keytool -list -v -keystore $JAVA_HOME/jre/lib/security/cacerts
```

### (5) Importar novo CA para certificados confiáveis

```
keytool -import -trustcacerts -file /path/to/ca/ca.pem -alias CA_ALIAS -keystore $JAVA_HOME/jre/lib/security/cacerts
```
