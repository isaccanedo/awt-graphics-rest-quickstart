# Serviço da Web para imagens com marca d'água

Este início rápido demonstra um caso de uso para [extensão Quarkus AWT](https://github.com/quarkusio/quarkus/tree/main/extensions/awt).

Há um ponto de extremidade POST único que consome dados de um formulário de várias partes e retorna um fluxo de octetos com uma imagem PNG com marca d'água.
Por uma questão de brevidade, independentemente do tipo de imagem postada, o serviço sempre retorna uma imagem PNG.

[Extensão Quarkus AWT](https://github.com/quarkusio/quarkus/tree/main/extensions/awt) habilita um conjunto de ImageIO e AWT
funcionalidade em imagens nativas do Quarkus. Consulte a documentação e os testes da extensão para conhecer o escopo disponível.
Dada a natureza das bibliotecas nativas no JDK implementando vários algoritmos de processamento de imagem,
aventurar-se fora do escopo testado pode resultar em tempo de construção de imagem nativa ou falha de tempo de execução.

# Dependências adicionais do sistema
Observação `microdnf` comando para instalar a biblioteca `fontconfig` em [Dockerfile.jvm](./src/main/docker/Dockerfile.jvm)
e [Dockerfile.legacy-jar](./src/main/docker/Dockerfile.legacy-jar) para suportar o modo jvm.
As bibliotecas `freetype` e `fontconfig` são necessárias para o modo nativo em [Dockerfile.native](./src/main/docker/Dockerfile.native).

# Uso com curl

e.g.

```bash
curl -F "image=@/tmp/my_image.jpg"  http://localhost:8080/watermark --output /tmp/result.png
```
Marca d'água a imagem fornecida com algum texto no canto superior esquerdo e um ícone do Quarkus no canto inferior direito.

# Uso com um código de cliente

Veja [ImageResourceTest.java](./src/test/java/org/acme/awt/rest/ImageResourceTest.java). The test is executed
in native mode with:

```bash
./mvnw clean verify -Pnative
```
Para executar testes nativos localmente, é necessário um JDK 11.0.13+ com Mandrel (ou GraalVM) 21.3+.
Além disso, as bibliotecas `freetype-devel` e `fontconfig` devem ser instaladas.

# Como é o resultado

This is an example of what this quick start does to an image:

![Alt text](./doc/example.png)
