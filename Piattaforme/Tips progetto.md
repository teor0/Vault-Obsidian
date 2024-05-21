# Lomboc
Attraverso lomboc posso evitare di scrivere getter, setter, hashcode, equals e tostring, questo è molto comodo e basta aggiungere le rispettive annotazioni prima della classe. Ad esempio:
```Java
@Getter
@Setter
@EqualsAndHashCode
@ToString
@entity
public class Product{

}
```
# File application.yaml
Nel file application.yaml vengono definiti parti importanti ed utili per il progetto come ad esempio, l'utilizzo di SSL per un certificato HTTPS, il livello di security, il datasource e url del database e come fare logging. Inoltre c'è la possibilità di specificare il path delle immagini in modo globale attraverso i seguenti tag
```
paths:
	images: progetto/pictures
```
che vanno in combinazione con l'annotazione @Value("$(path.images)")

# Entities
È buona norma per i campi delle entities specificare all'interno dell'annotazione @Column, la lunghezza del campo tramite lenght come quella definita sul db. Questo fa si che dopo di una persist, nel caso in cui il campo è più lungo della specifica del db, spring si occupa in automatico dell'eccezione.
L'annotazione @JsonIgnore ignora alcune informazioni che verranno ritornate magari dopo il login di un user.
L'annotazione @ToString.Exclude permette di escludere dal toString il campo annotato.