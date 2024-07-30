@Size la uso al posto di @Column(lenght=...) perché size è validante, stesso discorso per @NotNull e @Column(nullable=false) così che la validazione avvenga prima che hibernate faccia una query.
Anche se magari è meglio usare i DTO, non uso DTO nei service. Se li userò li userò nei controller

## Definizione di bean in spring
In Spring, the objects that form the backbone of your application and that are managed by the Spring IoC container are called beans. A bean is an object that is instantiated, assembled, and otherwise managed by a Spring IoC container. This definition is concise and gets to the point but fails to elaborate on an important element: the Spring IoC container.
Simply put, (IoC) is a process in which an object defines its dependencies without creating them. This object delegates the job of constructing such dependencies to an IoC container.

## Optional
`optional=false` is a runtime instruction. The primary functional thing it does is related to Lazy Loading. You can't lazy load a non-collection mapped entity unless you remember to set optional=false (because Hibernate doesn't know if there should be a proxy there or a null, unless you tell it nulls are impossible, so it can generate a proxy.)
## Autowired
L'annotazione autowired viene usata nei service per indicare a spring, che si vuole avere un'istanza di un repository gestita da esso. Spring andrà quindi a gestire tale istanza in particolare, se non esiste ne crea una e l'assegna alla variabile, se esiste la va a recuperare dal pool di istanze gestite e l'assegna alla variabile.

## Tipi di cascade
Le operazioni che verranno effettuate in cascata da una entity "padre" ad una entity figlio, sono le seguenti:
1. ALL: tutte le operazioni vengono propagate.
2. PERSIST: solo le operazioni di persist.
3. MERGE: solo le operazioni di MERGE.
4. REMOVE: solo le operazioni di REMOVE.
5. DELETE: è l'alternativa di JPA a REMOVE.
6. DETACH: come il padre uscirà dal persistent context, lo farà anche il figlio.
7. REFRESH: quando il padre refresha il db, anche il figlio farà una refresh.

## Differenza tra OnDelete e Cascade.remove
Supponiamo di avere 2 entity, l'entity casa e l'entity porta. Tramite Cascade.remove, se elimino la casa allora la porta associata verrà eliminata pure. Se invece ho OnDelete nell'entity porta associata al campo casa, se elimino la porta allora anche la casa verrà cancellata. In sostanza cascade propaga dal padre al figlio mentre OnDelete propaga dal figlio al padre.

## Save
Il metodo save() permette di rendere persistente i dati sul DB. Se devo fare delle modifiche posso usare save per fare l'update sul DB, inoltre se si lavora in un ambiente Transactional, non è obbligatorio usare save(). Questo perché se si usa findById() per prendere una entity dentro un metodo transactional, l'entity sarà già gestita dal persistence manager.

# Lock
Allora per i lock si possono usare due strategie fondamentalmente:
1. Usare l'entity manager in modo esplicito attraverso i lock programmatici. ![[lockem.jpg]] Questo approccio potrebbe portare a gestire troppa roba tra singleton entity manager ed entity.
2. Usare i lock tramite repository spring. ![[lockspring.jpg]] Di norma il metodo `findById()` vede se c'è il campo version ed usa il lock ottimistico ma si può tranquillamente ridefinire il metodo ed annotarlo con `@Lock` e la modalità preferità per abilitare il locking su quel metodo.

## Meccanismo post
``` Java
@PostMapping(consumes = {"application/json"})  
public ResponseEntity create(@RequestBody UtenteDTO dto){  
        UtenteDTO u= new UtenteDTO();  
    try{  
        u.setId(dto.getId());  
        u.setName(dto.getName());  
        u.setEmail(dto.getEmail());  
        System.out.println(u.getName());  
    }  
    catch(Exception e){  
        return new ResponseEntity<>("Error unknown",HttpStatus.BAD_REQUEST);  
    }  
    return new ResponseEntity<>(u,HttpStatus.OK);  
}
```
La post prende dal payload JSON gli attributi con lo **stesso** nome, e li mappa sull'oggetto che si vuole. Nel esempio mappa il seguente JSON nell'oggetto UtenteDTO:
``` JSON
{
	"id":"1",
	"name":"Ruggero",
	"email":"mail@mail.xyz"
}
```

# PRENDE IL TOKEN
Per prendere il token bisogna abilitare per prima cosa il service account role come in figura:
![[token1.jpg]] una volta attivato è possibile sceglie le credenziali con cui il client può autenticarsi, nel nostro caso client id e client secret ![[token2.jpg]]. Dopo di che occorre andare nel tab service accounts roles ed aggiungere il ruolo manage-users. PER AGGIUNGERLO OCCORRE FILTRARE come in figura: ![[token3.jpg]] questo perché i dev hanno le corna. Fatto questo ANCHE LE RICHIESTE TRAMITE GRANT_TYPE=PASSWORD necessitano di client id e client secret :).