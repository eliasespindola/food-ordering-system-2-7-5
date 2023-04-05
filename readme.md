## Diagrama das classes
- ![Captura de Tela 2023-04-01 às 13.54.25.png](Captura%20de%20Tela%202023-04-01%20%C3%A0s%2013.54.25.png)

## Explicacoes
- Ele criar um base entity
  - Classe para ser base para as entidades com tudo generico
- Ele cria um aggregateRoot
  - Eu quero marcar a raiz agregada de uma agregação apenas estendendo essa classe abstrata.
  - Então, quando eu olhar para o código, poderei dizer qual classe é uma entidade e qual é o agregado raiz
  - No AggregateRoot, vou simplesmente estender o BaseEntity para poder reutilizar o getter e o setter
  - Portanto, esta será simplesmente uma classe de marcador.
  - é AggregateRoot, para distinguir o objeto raiz das outras entidades.
  - Vou usar essas duas classes, BaseEntity e AggregateRoot das classes de entidade que vou defina no núcleo do domínio de serviço do pedido.
  - Além disso, quando eu implementar os módulos principais de domínio de serviço de pagamento e restaurante, usarei novamente esses
- Uso do compareTo
  - Use isto quando for comparar big decimal
- A classe order no order-domain-core
  - Ele vai servir para: Esta será minha raiz agregada para o processo de pedido, então estenderei a classe abstrata AggregateRoot
  - a propriedade ID do AggregateRoot será definida como OrderId e será herdada na classe de order
  - E a classe order vai se basear na fotinha que esta acima
## Temos um plugin chamado InnerBuilder que nós ajuda a criar builders

## Maneiras de publicar os eventos


### Maneira 1

- Criar um publicador para cada evento e assim vamos garantir que ele vai enviar este evento
- Podemos usar um proxy  na hora que formos persistir a transação
- Temos que ter o @Transactional
- Temos a @TransactionalEventListener
  - Temos uma anotação que ouve um evento que é disparado de um metodo transacional e só processa os eventos se a operação transacional for concluida com sucesso!
  - Ele cria uma classe e implementa a interface **ApplicationEventPublisherAware**
  - ![image](https://user-images.githubusercontent.com/30422473/229913728-7527946a-6372-4c26-a3e2-8b365201b418.png)
  - Ele cria um cara para ficar ouvindo 
    - ![image](https://user-images.githubusercontent.com/30422473/229914026-3e7b9033-01b0-410d-bbb7-68c759dda88e.png)
    - E injeta na classe que queremos para fazer a publicacao do evento


## Maneira de ver o covarage da classe
- ![image](https://user-images.githubusercontent.com/30422473/229914597-c891c56c-43ef-4885-bd4c-0b73497b6e0c.png)

## O que é o kafka?
- Kafka pode replicar os dados em diferentes nós e aumentar a resiliência do sistema.
- Kafka tem o conceito de tópico, que é uma estrutura lógica de dados que consiste em partições.
- E as partições são a menor unidade de armazenamento físico que contém os dados.
- Kafka tem duas características importantes. Uma delas é a resiliência.
- A segunda característica importante é o fácil dimensionamento.Você pode ter threads consumidores paralelos até o número da partição em um tópico. Isso significa que se você criar uma nova partição, poderá criar um novo consumidor e consumir os dados com um nova thread simultaneamente.
- Por fim, conforme mencionado, os dados são inseridos como um log apenas de anexo nas partições. E uma vez inserido os dados não podem ser alterados ou atualizados. Portanto, é imutável.
- O kafka tem os initializer dele no pacote de infrastructure
- Vamos fazer os seguintes passos
  -  docker-compose -f common.yml -f zookeeper.yml up
  -  echo ruok | nc localhost 2181
  -  docker-compose -f common.yml -f kafka_cluster.yml up
  -  docker-compose -f common.yml -f init_kafka.yml up
  -  Vamos configurar em localhost:9000
    -   add cluster
    -   cluster name - food-ordering-system-cluster
    -   cluster zookeeper - zzookeeper:2181
    -   save

## Duvidas
- ZoneDateTime
- Callback
- PreDestroy
- 
